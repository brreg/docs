---
title: Uthenting av meldinger
description: Beskrivelser av API innen BRs elektroniske mottak av meldinger
weight: 100
---

## Innledning

Brønnøysundregistrenes elektroniske mottak har et REST-grensesnitt som kan benyttes av eksterne parter for innsending av meldinger.

## Sikkerhetsmekanismer

Siden dette er begrensede API så skal kallende parter autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_overordnet.html).

For å kunne få tilgang til våre begrensede APIer må man bruke et JWT-token fra Maskinporten med scopet `brreg:mottak`

Access-tokenet oppgis i headeren `Authorization`. Husk `Bearer` før tokenet.

| Header        | Verdi                       |
|---------------|-----------------------------|
| Authorization | Bearer <maskinporten-token> |

## Grensesnittbeskrivelse

[Swagger](https://mottak.brreg.no/outbound/swagger-ui/index.html)

Tjenesten benytter seg av standard HTTP GET og POST.

| HTTP-metode | URL                                                           | Content-type             | Beskrivelse                                                                                    | Sikret med jwt |
|:------------|:--------------------------------------------------------------|:-------------------------|:-----------------------------------------------------------------------------------------------|:---------------|
| GET         | https://mottak.brreg.no/outbound/available                    | application/json         | Lister ut tilgjengelige meldinger (med mottakId) for organisasjonsnummer oppgitt i JWT tokenet | JA             |
| GET         | https://mottak.brreg.no/outbound/download?mottakId={mottakId} | application/octet-stream | Laster ned forsendelse med oppgitt mottakId                                                    | JA             |
| PUT         | https://mottak.brreg.no/outbound/confirm?mottakId={mottakId}  | application/json         | Bekrefter at forsendelse med oppgitt mottakId er lastet ned av klient                          | JA             |

### /available

Endepunktet returnerer tilgjengelige forsendelser for organisasjonsnummer som er oppgitt i JWT-tokenet.

#### Response

Ved 200 OK:

```json
[
  {
  "mottakId":"be935814-c7a3-4a9f-8bbc-ac278cbe41d5",
  "version":0,
  "orgnr":910514350,
  "dokumentId":"be935814-c7a3-4a9f-8bbc-ac278cbe41d5",
  "status":"ready",
  "oppdatert":"2019-09-05T09:43:51.691"
  }
]
```

### /download?mottakId={mottakId}

Endepunktet returnerer ZIP-fil med Melding for angitt mottakId. MottakId er en UUID.

#### Response

Bytestream som APPLICATION_OCTET_STREAM

### /confirm?mottakId={mottakId}

Endepunktet bekrefter forsendelsen med angitt mottakId som nedlastet. MottakId er en UUID. 

Denne forsendelsen vil da ikke lenger fremkomme ved kall til `/available`. 

#### Response

200 OK ved success.

## Feilmeldinger

| HTTP-kode                 | Applikasjonsfeilkode | Feilmelding                                                                                                                                                                                                   |
|:--------------------------|:---------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 500 Internal Server Error | ERROR-00005          | Optimistic lock exception. Hvis samme forsendelseinfo blir forsøkt confirmed nedlastet samtidig kan dette skje. <br> I utgangspunktet kan man se bort i fra denne, men å forhindre dette er klientens ansvar. |

Disse kommer på JSON-formatet:

```json
{
  "feilId":"72577aa8-0ba1-4424-a310-fd9671547953",
  "mottakId":"fe7234ec-b51f-47d1-a414-5b17123118b3",
  "kilde":"maskinport-agent",
  "feilkode":"ERROR-00005",
  "beskrivelse": "Simultaneous attempt to confirm same file"
}
```

**I tillegg kommer 401 - Unauthorized ved mangler på Bearer token.**

| HTTP-kode           | header           | Header-value                                                                                                                   | Forklaring                                                                                                                      |
|:--------------------|:-----------------|:-------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------|
| 401 - Unauthorized  | WWW-Authenticate | Bearer realm="unspecified", error="unauthorized", error_description="Full authentication is required to access this resource"  | JWT access token ikke oppgitt i Authorization header i request.                                                                 |
| 401 - Unauthorized  | WWW-Authenticate | Bearer realm="unspecified", error="invalid_token", error_description="invalid bearer token or wrong scope for bearer token"    | JWT access token er oppgitt, men det er enten ugyldig (utgått, korrupt eller gjeldende for et annet scope en tjenesten krever). |

