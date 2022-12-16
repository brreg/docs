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

| HTTP-metode | URL                                                                         | Beskrivelse                                                                                                                                                                                      |
|:------------|:----------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GET         | https://\{domene\}/api/partner/reelle-rettigheter/{organisasjonsnummer}     | Hent opplysninger om en reell rettighet på angitt organisasjonsnummer. <br/>En reell rettighet for en gitt virksomhet inneholder en liste med reelle rettighetshavere, hvis dette er registrert. |
| GET         | https://\{domene\}/api/partner/reelle-rettigheter/totalbestand/json         | Hent alle registrerte opplysninger i registeret i form av JSON. Returnerer JSON i en ZIP-fil.                                                                                                    |
| GET         | https://\{domene\}/api/partner/reelle-rettigheter/totalbestand/csv          | Hent alle registrerte opplysninger i registeret i form av CSV. Returnerer CSV i en ZIP-fil.                                                                                                      |


**Domener**:

* For testmiljø : `https://rrh.ppe.brreg.no`
* For produksjon: `https://rrh.brreg.no`

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer. Forespørselen valideres og returnerer opplysninger om reelle rettighetshavere, inklusive fødselsnummer og d-nummer, på oppgitt organisasjonsnummer.

### Testdata
Se [underside for testdata]({{<ref "testdata_for_partner_api.md">}}). Her finner du organisasjonsnummer du kan bruke bruke i vårt testmiljø og hvilke data du får i retur.

#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.

#### Validering

* Forespørselen skal alltid inneholde organisasjonsnummeret det gjøres oppslag på.
* Dersom forespørselen inneholder et organisasjonsnummer som ikke er lovlig oppbygd, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 samt et dokument (på JSON-format) i retur. JSON-dokumentet inneholder opplysninger om reelle rettighetshavere.


##### Eksempelrespons for oppslag på organisasjonsnummer
***Eksempelresponsen kan endre seg***
```json
{
   "registreringId": "83201f83-b92a-484c-a92c-3d5736fd1adc",
   "registreringStatus": {
      "kode": "registreringstatus.regi",
      "kodetekst": "Reelle rettighetshavere er registrert"
   },
   "registrertDato": "2022-12-15T12:00:06.231509Z",
   "reelleRettighetshavereStatus": {
      "kode": "reellerettighetshaverestatus.arid",
      "kodetekst": "Virksomheten har meldt at de har reelle rettighetshavere, og at alle reelle rettighetshavere er identifisert"
   },
   "registreringspliktigVirksomhet": {
      "organisasjonsnummer": "111111111"
   },
   "reelleRettighetshavere": [
      {
         "folkeregistrertPerson": {
            "foedselsEllerDNummer": "23456789012",
            "foedselsdato": "2002-11-05",
            "foedselsaar": "2002",
            "navn": {
               "fornavn": "STOLT EFFEKTIV",
               "mellomnavn": "KUL",
               "etternavn": "PARASOLL"
            },
            "erDoed": false,
            "statsborgerskap": [
               {
                  "landkode": "NOR",
                  "land": "Norge"
               },
               {
                  "landkode": "MEX",
                  "land": "Mexico"
               }
            ]
         },
         "bostedsland": {
            "landkode": "NOR",
            "land": "Norge"
         },
         "erUnntattFraInnsyn": false,
         "posisjoner": [
            {
               "type": {
                  "kode": "posisjontype.eier",
                  "kodetekst": "Eierskap"
               },
               "stoerrelseIntervall": {
                  "kode": "stoerrelseintervall.int2",
                  "kodetekst": "50% - 74,99%"
               },
               "grunnlag": [
                  {
                     "kode": "grunnlagtype.dire",
                     "kodetekst": "Direkte"
                  }
               ]
            }
         ],
         "foerstRegistrertDato": "2022-12-16T12:00:06.242Z",
         "endretDato": "2022-12-16T12:00:06.242Z"
      },
      {
         "utenlandskPerson": {
            "foedselsdato": "1983-03-24",
            "foedselsaar": "1983",
            "fulltNavn": "GILL BATES",
            "statsborgerskap": [
               {
                  "landkode": "DEU",
                  "land": "Tyskland"
               },
               {
                  "landkode": "SWE",
                  "land": "Sverige"
               },
               {
                  "landkode": "USA",
                  "land": "USA"
               }
            ]
         },
         "bostedsland": {
            "landkode": "USA",
            "land": "USA"
         },
         "erUnntattFraInnsyn": false,
         "posisjoner": [
            {
               "type": {
                  "kode": "posisjontype.kont",
                  "kodetekst": "Kontroll over stemmerettigheter"
               },
               "stoerrelseIntervall": {
                  "kode": "stoerrelseintervall.int1",
                  "kodetekst": "25,01% - 49,99%"
               },
               "grunnlag": [
                  {
                     "kode": "grunnlagtype.indi",
                     "kodetekst": "Indirekte"
                  },
                  {
                     "kode": "grunnlagtype.enav",
                     "kodetekst": "Enighet eller avtale"
                  }
               ]
            },
            {
               "type": {
                  "kode": "posisjontype.ruas",
                  "kodetekst": "Rett til å utpeke eller avsette minst halvparten av styremedlemmene"
               },
               "grunnlag": [
                  {
                     "kode": "grunnlagtype.enav",
                     "kodetekst": "Enighet eller avtale"
                  }
               ]
            }
         ],
         "foerstRegistrertDato": "2022-12-16T12:00:06.242Z",
         "endretDato": "2022-12-16T12:00:06.242Z"
      },
      {
         "folkeregistrertPerson": {
            "foedselsEllerDNummer": "12345678901",
            "foedselsdato": "1971-07-18",
            "foedselsaar": "1971",
            "navn": {
               "fornavn": "MINIMALISTISK",
               "etternavn": "HANDLELISTE"
            },
            "erDoed": false,
            "statsborgerskap": [
               {
                  "landkode": "MSR",
                  "land": "Montserrat"
               }
            ]
         },
         "bostedsland": {
            "landkode": "NOR",
            "land": "Norge"
         },
         "erUnntattFraInnsyn": false,
         "posisjoner": [
            {
               "type": {
                  "kode": "posisjontype.anne",
                  "kodetekst": "Kontroll på annen måte"
               },
               "grunnlag": [],
               "beskrivelseAnnenMaate": "Beskrivelse av hva kontrollen går ut på."
            }
         ],
         "foerstRegistrertDato": "2022-12-16T12:00:06.251Z",
         "endretDato": "2022-12-16T12:00:06.251Z"
      }
   ]
}
```
### Totalbestand

#### Beskrivelse

Henter ut alle gjeldende opplysninger i registeret i form av CSV eller JSON i en ZIP-fil. Filene blir oppdatert en gang i døgnet.


#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.

#### Response

Dersom kallet lykkes får man HTTP-status 200 samt en Zippet fil (på JSON- eller CSV-format) i retur. Filen inneholder alle gjeldende opplysninger i Register over reelle rettighetshavere.  
**I vårt testmiljø kan filen inneholde flere elementer en de som er beskrevet på vår side om [testdata]({{<ref "testdata_for_partner_api.md">}}).** 

##### Eksempelrespons for totalbestand
Om man henter ut totalbestand som JSON, vil filen være en liste der elementene i listen er på samme format som endepunktet `Oppslag på organisasjonsnummer`.  
**Eksempelfil på JSON-format kan lastes ned her snart**

Om man henter ut totalbestand som CSV, vil man få en kommaseparert fil som kan åpnes i for eksempel Excel.  
**Eksempelfil på CSV-format kan lastes ned her snart**

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
