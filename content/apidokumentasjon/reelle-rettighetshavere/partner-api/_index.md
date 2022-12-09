---
title: Partner API
description: Beskrivelse av partner API for Register over reelle rettighetshavere
weight: 100
---

## Innledning
Brønnøysundregistrene tilbyr en lukket, standardisert maskin-til-maskin-tjeneste (API) som kan benyttes av eksterne konsumenter for innsyn i Register over reelle rettighetshavere.

Denne dokumentasjonen viser hvordan eksterne systemer kan integrere seg mot APIet, og hvordan man benytter seg av tjenesten for å hente data.


***Denne siden er fortsatt under utvikling.***

## API-referanse
Denne tjenesten tilbyr informasjon om reelle rettighetshavere ved oppslag på organisasjonsnummer, inklusive fødselsnummer eller D-nummer.
Tjenesten skjermer ikke informasjon om mindreårige og andre som er unntatt fra innsyn.

Se gjerne på [OpenAPI-spesifikasjon](https://github.com/brreg/openAPI/blob/master/specs/reelle-partner-api.yaml) for teknisk beskrivelse av tjenesten.

*Lenker til Swagger-dokumentasjon kommer her.*


## Hvordan få tilgang

For å få tilgang til partner API må du sende e-post til `opendata.rrh@brreg.no`. I e-posten må du opplyse om hvilket organisasjonsnummer det gjelder, og hvilken hjemmel til utvidet tilgang virksomheten faller inn under.  
Hvis tilgangen gjelder testmiljø må du i tillegg oppgi hvilken ip-adresse dere kommer fra da API'ene i test har ip-filtrering.

## Disse kan få tilgang til APIet

### Offentlige myndigheter nevnt i forskriften § 3-11:

[Lovdata - Forskrift til lov om register over reelle rettighetshavere](https://lovdata.no/dokument/SF/forskrift/2021-06-21-2056?q=reelle%20rettighetshavere)

a) politi- og påtalemyndighet  
b) enheten for finansiell etterretning ansvarlig for å motta opplysninger om mistenkelige forhold etter hvitvaskingsloven § 26  
c) skattemyndigheter  
d) tilsynsmyndigheter for rapporteringspliktige etter hvitvaskingsregelverket  
e) andre myndigheter med ansvar for å etterforske og påtale hvitvasking, primærforbrytelser og terrorfinansiering  
f) andre myndigheter med ansvar for sporing, båndlegging og inndragning av utbytte  
g) sikkerhetsmyndigheten  
h) tilsynsmyndighet for stiftelser



### Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav a, b, c, e, g, h til k, n og o:

a) bank  
b) kredittforetak  
c) finansieringsforetak  
e) e-pengeforetak  
g) betalingsforetak og andre som har rett til å yte betalingstjenester  
h) verdipapirforetak  
i) forvaltningsselskap for verdipapirfond  
j) forsikringsforetak  
k) foretak som driver forsikringsformidling som ikke er gjenforsikringsmegling  
n) forvalter av alternative investeringsfond  
o) låneformidlingsforetak

## Sikkerhetsmekanismer
Siden dette er et Partner API må konsumenter autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_guide_apikonsument.html).

For å kunne få tilgang til våre Partner API er det tre forutsetninger.

1. Virksomhetssertifikat
2. Registrert klient hos Maskinporten
3. I dialogen med Brønnøysundregistrene om å få tilgang til API'et vil din virksomhet ha fått informasjon om hvilket av de to scopene virksomheten har fått tilgang til:
JWT-token fra Maskinporten mot ett av disse scopene:
   1. `brreg:reelle/partner.offentlig`
   2. `brreg:reelle/partner.rapporteringspliktig`

Tokenet som hentes fra Maskinporten må bli sendt som autorisasjonstoken (Bearer token) når et kall mot tjenesten blir utført.

Se [veiledning for integrasjon mot Maskinporten]({{<ref "mp-integrasjonsveiledning.md">}}).

[Regelverk](https://lovdata.no/dokument/SF/forskrift/2021-06-21-2056?q=forskrift%20reelle%20rettighetshavere): Hjemler for tilgjengeliggjøring av data fra Brønnøysundregistrene.
## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                       | Beskrivelse                                                                                                                                                                                      |
|:------------- |:--------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/partner/reelle-rettigheteter/{organisasjonsnummer} | Hent opplysninger om en reell rettighet på angitt organisasjonsnummer. <br/>En reell rettighet for en gitt virksomhet inneholder en liste med reelle rettighetshavere, hvis dette er registrert. |


**Domener**:

* For testmiljø : `https://rrh.ppe.brreg.no`
* For produksjon: `https://rrh.brreg.no`

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer. Forespørselen valideres og returnerer opplysninger om reelle rettighetshavere, inklusive fødselsnummer og d-nummer, på oppgitt organisasjonsnummer.

#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.

#### Validering

* Forespørselen skal alltid inneholde organisasjonsnummeret det gjøres oppslag på.
* Dersom forespørselen inneholder et organisasjonsnummer som ikke er lovlig oppbygd, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 samt et dokument (på JSON-format) i retur. JSON-dokumentet inneholder opplysninger om reelle rettighetshavere.


##### Eksempelrespons for oppslag på organisasjonsnummer
***Eksempelresponsen er kun et utkast, og strukturen kan endre seg***
```json
{
   "registreringId": "1f92ac29-7b4f-4f6b-b402-6e9bc7a3ff59",
   "registreringStatus": {
      "kode": "registreringstatus.regi",
      "beskrivelse": "Reelle rettighetshavere er registrert"
   },
   "gjelderFraDato": "2022-09-06T09:17:39.87542Z",
   "reelleRettighetshavereStatus": {
      "kode": "reellerettighetshaverestatus.arid",
      "beskrivelse": "Alle reelle rettighetshavere kan identifiseres"
   },
   "reelleRettighetshavere": [
      {
         "foedselsEllerDNummer": 12345678901,
         "foedselsdato": "2002-11-05",
         "foedselsaar": "2002",
         "navn": {
            "fornavn": "STOLT EFFEKTIV",
            "mellomnavn": "KUL",
            "etternavn": "PARASOLL",
            "fulltNavn": "STOLT EFFEKTIV KUL PARASOLL"
         },
         "foerstRegistrertDato": "2022-09-06T09:17:39.275205Z",
         "endretDato": "2022-09-06T09:17:39.275205Z",
         "statsborgerskap": [
            {
               "landkode": "NOR",
               "land": "Norge"
            },
            {
               "landkode": "MEX",
               "land": "Mexico"
            }
         ],
         "bostedsland": {
            "landkode": "NOR",
            "land": "Norge"
         },
         "erDoed": false,
         "erUnntattFraInnsyn": false,
         "posisjoner": [
            {
               "posisjonType": {
                  "kode": "posisjontype.eier",
                  "beskrivelse": "Eierskap"
               },
               "stoerrelseIntervall": {
                  "kode": "stoerrelseintervall.int2",
                  "beskrivelse": "50% - 74,99%"
               },
               "grunnlag": [
                  {
                     "grunnlagType": {
                        "kode": "grunnlagtype.dire",
                        "beskrivelse": "Direkte"
                     }
                  },
                  {
                     "grunnlagType": {
                        "kode": "grunnlagtype.indi",
                        "beskrivelse": "Indirekte"
                     }
                  }
               ]
            }
         ]
      },
      {
         "foedselsdato": "1983-12-01",
         "foedselsaar": "1983",
         "navn": {
            "fulltNavn": "TOM SVENSKE NELSON"
         },
         "foerstRegistrertDato": "2022-09-06T09:17:39.275205Z",
         "endretDato": "2022-09-06T09:17:39.275205Z",
         "statsborgerskap": [
            {
               "landkode": "SWE",
               "land": "Sverige"
            }
         ],
         "bostedsland": {
            "landkode": "SWE",
            "land": "Sverige"
         },
         "erDoed": false,
         "erUnntattFraInnsyn": false,
         "posisjoner": [
            {
               "posisjonType": {
                  "kode": "posisjontype.eier",
                  "beskrivelse": "Eierskap"
               },
               "stoerrelseIntervall": {
                  "kode": "stoerrelseintervall.int1",
                  "beskrivelse": "25,01% - 49,99%"
               },
               "grunnlag": [
                  {
                     "grunnlagType": {
                        "kode": "grunnlagtype.indi",
                        "beskrivelse": "Indirekte"
                     }
                  }
               ]
            },
            {
               "posisjonType": {
                  "kode": "posisjontype.ruas",
                  "beskrivelse": "Rett til å utpeke eller avsette minst halvparten av styremedlemmene"
               },
               "grunnlag": [
                  {
                     "grunnlagType": {
                        "kode": "grunnlagtype.enav",
                        "beskrivelse": "Enighet eller avtale"
                     }
                  }
               ]
            }
         ]
      }
   ]
}
```

---


## HTTP-statuskoder

| HTTP-kode                 | Beskrivelse                                                                                                                                                                         |
|:--------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200 OK                    | Henting av data gikk bra                                                                                                                                                            |
| 400 Bad Request           | Feil i spørring. Applikasjonen vil gi en detaljert feilmelding for hva som er feil med spørring                                                                                     |
| 403 Forbidden             | Feil ved autentisering eller autorisering. Bearer-tokenet som ble sendt inn er ikke gyldig eller virksomheten har ikke fått tilgang til scope for tjenesten                         |
| 404 Not Found             | Virksomheten har ikke registrert reelle rettighetshavere                                                                                                                            |
| 500 Internal Server Error | Intern feil i tjenesten, for eksempel at en underliggende datakilde ikke svarer                                                                                                     |

## Ordliste

Definisjoner på begrep som er brukt i denne dokumentasjonen.

| Begrep              | Definisjon                                                                                                          |
|:--------------------|:--------------------------------------------------------------------------------------------------------------------|
| API                 | Programmeringsgrensesnitt                                                                                           |
| Partner API         | Et API som krever autentisering/autorisering (for eksempel ved bruk av Maskinporten)                                |
| Reell rettighet     | En reell rettighet for en gitt virksomhet inneholder en liste med reelle rettighetshavere, hvis dette er registrert |
| HTTP                | Datakommunikasjonsstandard                                                                                          |
| HTTP-statuskoder    | Statuskoder for datakommunikasjonsstandard                                                                          |
| REST                | Datakommunikasjonmønster                                                                                            |
| JSON                | Åpen standard for dataformat                                                                                        |
| Organisasjonsnummer | Identifikasjonsnummer for virksomhet                                                                                |

---
