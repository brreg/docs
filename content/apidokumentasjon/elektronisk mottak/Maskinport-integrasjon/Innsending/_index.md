---
title: Innsending av meldinger
description: Beskrivelser av API innen BRs elektroniske mottak av meldinger
weight: 100
---

## Innledning

Brønnøysundregistrenes elektroniske mottak har et REST-grensesnitt som kan benyttes av eksterne parter for innsending av meldinger.

## Sikkerhetsmekanismer

Siden dette er begrensede API så skal kallende parter autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_overordnet.html).

For å kunne få tilgang til våre begrensede APIer må man bruke et JWT-token fra Maskinporten med scopet `brreg:mottak`

Access-tokenet oppgis i headeren `Authorization`. 
Husk `Bearer` før tokenet.

| Header        | Verdi                       |
|---------------|-----------------------------|
| Authorization | Bearer <maskinporten-token> |

## Grensesnittbeskrivelse

[Swagger](https://mottak.brreg.no/inbound/swagger-ui/index.html)

| HTTP-metode | URL                                                   | Beskrivelse                                  | Sikret med jwt |
|:------------|:------------------------------------------------------|:---------------------------------------------|:---------------|
| POST        | https://mottak.brreg.no/inbound/upload                | Sender inn melding med 0 eller flere vedlegg | JA             |

### /upload

Denne forespørselen laster opp en melding med ingen eller flere vedlegg/attachments.

Endepunktet tar i mot **POST** multipart-requester med følgende deler:

| Felt          | Type           | Innhold                                                                                   | Påkrevd |
|---------------|----------------|-------------------------------------------------------------------------------------------|---------|
| Authorization | Header         | JWT access token                                                                          | Ja      |
| payload       | form-data      | XML i henhold til Melding ([Link til XSD](http://schema.brreg.no/postmottak/melding.xsd)) | Ja      |
| attachments   | multipart-file | fil/bytestream                                                                            | Nei     |

#### Response

Ved 200 OK:

```json
{
  "mottakId": "36b5516f-ecd4-4948-9586-42f4b7d3198a",
  "mottattTidspunkt": "2019-09-02T13:18:40.785",
  "antallVedlegg": 2
}
```
#### Filtyper som støttes:
XML, PDF, DOC, DOCX, XLS, XLSX, RTF, JPEG, PNG, ODT, ODS, TIFF, TXT, JSON, CSV, ZIP og GZIP.

#### Maks request-størrelse:
35 MB 

#### Feilmeldinger

| HTTP-kode                   | Applikasjonsfeilkode | Feilmelding                                                                   |
|:----------------------------|:---------------------|:------------------------------------------------------------------------------|
| 500 Internal Server Error   | ERROR-00000          | Generisk feilhåndterer. Forsøk igjen senere. Hvis vedvarende, kontakt support |
| 400 Bad Request             | CLIENTERROR-10001    | Melding kunne ikke behandles, feilet i XML-validering                         |
| 400 Bad Request             | CLIENTERROR-10002    | Mangler med request (f.eks. manglende payload)                                |
| 413 Request Entity Too Large| CLIENTERROR-10003    | Request is too large to upload                                                |
| 415 unsupported media type  |                      | Unsupported file type(s):                                                     |

Disse kommer på JSON-formatet:

```json
{
  "feilId":"72577aa8-0ba1-4424-a310-fd9671547953",
  "mottakId":"fe7234ec-b51f-47d1-a414-5b17123118b3",
  "kilde":"maskinport-agent",
  "feilkode":"ERROR-00003",
  "beskrivelse":"Message invalid according to schema"
}
```

**I tillegg kommer 401 - Unauthorized ved mangler på Bearer token.**

| HTTP-kode          | header           | Header-value                                                                                                                  | Forklaring                                                                                                                      |
|:-------------------|:-----------------|:------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------|
| 401 - Unauthorized | WWW-Authenticate | Bearer realm="unspecified", error="unauthorized", error_description="Full authentication is required to access this resource" | JWT access token ikke oppgitt i Authorization header i request.                                                                 |
| 401 - Unauthorized | WWW-Authenticate | Bearer realm="unspecified", error="invalid_token", error_description="invalid bearer token or wrong scope for bearer token"   | JWT access token er oppgitt, men det er enten ugyldig (utgått, korrupt eller gjeldende for et annet scope en tjenesten krever). |

### Eksempel 

#### Opprett HttpEntity

```java
MultiValueMap<String, String> fileMap = new LinkedMultiValueMap<>();
fileMap.add(HttpHeaders.CONTENT_DISPOSITION, ContentDisposition.builder("form-data")
        .name("attachments")
        .filename("filnavn.zip")
        .build()
        .toString());

HttpEntity<byte[]> fileEntity = new HttpEntity<>("filecontent".getBytes(), fileMap);
MultiValueMap<String, Object> body = new LinkedMultiValueMap<>();
body.add("attachments", fileEntity);
body.add("payload", new HttpEntity<String>(konvolutt));

HttpHeaders headers = new HttpHeaders();
headers.setContentType(MediaType.MULTIPART_FORM_DATA);

String token = bearerTokenProvider.getToken(scope); // Provides Maskinporten-token with correct scope
if (token != null) {
    headers.add("Authorization", "Bearer " + token);
}

HttpEntity<MultiValueMap<String, Object>> requestEntity = HttpEntity<>(body, headers);
```

#### Send HttpEntity

```java
ResponseEntity<String> objectResponseEntity = restTemplate.exchange("https://mottak.brreg.no/inbound/upload", HttpMethod.POST, requestEntity, String.class);
```

## Testmiljø

URL mot PPE-testmiljø er `https://mottak.ppe.brreg.no/inbound`
