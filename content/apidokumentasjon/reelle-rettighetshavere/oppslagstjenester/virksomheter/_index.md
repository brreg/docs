---
title: Virksomheter
description: Beskrivelse av tjeneste for oppslag/søk i Register over reelle rettighetshavere
weight: 100
---

## Innledning
Brønnøysundregistrene tilbyr en tilgangsstyrt tjeneste som kan benyttes av eksterne konsumenter for oppslag/søk i Register over reelle rettighetshavere.  
Oppslagstjenesten kalles "Virksomheter" pga ved oppslag eller søk vil man få returnert opplysninger om registrerte virksomheter og deres reelle rettighetshavere.  
Denne dokumentasjonen viser hvordan eksterne systemer kan integrere seg mot REST API'et til tjenesten.  

## API-referanse
API'et tilbyr opplysninger om registrerte virksomheter og deres reelle rettighetshavere ved oppslag på organisasjonsnummer, søk på fødsels-/D-nummer, eller ved nedlasting av fil med totalbestand.  
Opplysningene om reelle rettighetshavere inkluderer fullt fødsels- eller D-nummer fra Folkeregisteret.  
API'et skjermer ikke opplysninger om mindreårige og andre som er unntatt fra innsyn.  

### Swagger-dokumentasjon
* Testmiljø : https://rrh.ppe.brreg.no/api/oppslag/swagger-ui/index.html
* Produksjon : https://rrh.brreg.no/api/oppslag/swagger-ui/index.html

### OpenAPI-spesifikasjon
Nedlastbar OpenAPI-spesifikasjon finner du her:
* Testmiljø : https://rrh.ppe.brreg.no/api/oppslag/openapi/openapi.yaml
* Produksjon : https://rrh.brreg.no/api/oppslag/openapi/openapi.yaml

## Testdata
Se [underside for testdata]({{<ref "testdata_for_tilgangsstyrt_api.md">}}). Her finner du organisasjonsnummer du kan bruke bruke i vårt testmiljø og hvilke data du kan forvente å få i retur.  
NB! Vi må ta forbehold om at det kan skje noen endringer i testdata pga pågående intern testing, men målet er at disse testdataene i så stor grad som mulig skal være stabile.

## Grensesnittbeskrivelse

**Base URL**:
* Testmiljø : `https://rrh.ppe.brreg.no/api/oppslag`
* Produksjon: `https://rrh.brreg.no/api/oppslag`

| Navn                           | HTTP-metode | Endepunkt                                                                    | Beskrivelse                                                                                                                                                                                                                                                                                                                           |
|:-------------------------------|:------------|:-----------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Oppslag på organisasjonsnummer | GET         | https://\{baseurl\}/v1/virksomheter/{organisasjonsnummer}                    | Hent en registrert virksomhet med opplysninger om reelle rettighetshavere ved å angi organisasjonsnummer. Responsen inneholder en virksomhet med opplysninger om hvem som er registrert som reelle rettighetshavere på nåværende tidspunkt.                                                                                           |
| Søk på fødselsnummer           | GET         | https://\{baseurl\}/v1/virksomheter?foedselsnummer={fødsels- eller D-nummer} | Finn registrerte virksomheter der person med angitt fødsels-/D-nummer er reell rettighetshaver. Responsen inneholder en liste over virksomheter der angitt person er registrert som reell rettighetshaver på nåværende tidspunkt. Den angitte personen inngår som en av potensielt flere reelle rettighetshavere for hver virksomhet. |
| Last ned totalbestand          | GET         | https://\{baseurl\}/v1/virksomheter/totalbestand                             | Last ned fil som inneholder alle registrerte virksomheter med opplysninger om hvem som er reelle rettighetshavere. Endepunktet returnerer de sist oppdaterte opplysningene om hver virksomhet, og gir ikke ut historiske data. Endepunktet returnerer en ZIP-komprimert JSON-fil. Fil blir oppdatert en gang i døgnet.                |

### Oppslag på organisasjonsnummer

#### Request
Path-parameter "organisasjonsnummer" er påkrevd, og må være korrekt oppbygd. Hvis ikke vil du få http-status 400 (Bad request) i retur.

#### Response
* Dersom virksomheten er registrert i registeret vil oppslaget gi http-status 200 (OK) i retur samt en response-body på json-format.
* Dersom virksomheten ikke er registrert i registeret vil oppslaget returnere en http-status 404 (Not found).

### Søk på fødselsnummer

#### Request
Query-string "foedselsnummer" er påkrevd, og må være et korrekt oppbygd fødsels- eller D-nummer. Hvis ikke vil du få http-status 400 (Bad request) i retur.

#### Response
* Dersom personen du søker på er reell rettighetshaver i en eller flere registrerte virksomheter vil søket gi http-status 200 (OK) i retur samt en response-body på json-format.
* Dersom personen du søker på IKKE er reell rettighetshaver i noen virksomheter vil søket fortsatt returnere en http-status 200 (OK), og json response-bodyen vil inneholde en tom liste med virksomheter. 

### Last ned totalbestand

#### Request
Query-string "format" er påkrevd. Foreløpig er det kun "json" som kan angis som verdi da det er det eneste formatet vi pr nå støtter for totalbestand, men støtten kan bli utvidet i fremtiden. Hvis du angir en annen verdi vil du få http-status 400 (Bad request) i retur.

#### Response
Dersom du angir korrekt "format" som input vil kallet gi http-status 200 (OK) samt en zippet json-fil i retur. 

## HTTP-statuskoder
Nedenfor har vi listet opp de vanligste HTTP-statuskodene du kan forvente å få i retur i forskjellige sammenhenger.

| HTTP-kode                 | Beskrivelse                                                                                                                                                        |
|:--------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200 OK                    | Henting av data gikk bra                                                                                                                                           |
| 400 Bad Request           | Feil i spørring. Applikasjonen vil gi en detaljert feilmelding som beskriver hva som er feil med spørringen                                                        |
| 401 Unauthorized          | Feil ved autentisering eller autorisering. Bearer-tokenet som ble sendt inn er ikke gyldig eller virksomheten har ikke fått tilgang til scope for tjenesten        |
| 404 Not Found             | Ingen data funnet for angitte parametre. Dette kan feks indikere at virksomheten ikke har registrert reelle rettighetshavere                                       |
| 500 Internal Server Error | Intern feil i tjenesten, for eksempel at en underliggende datakilde ikke svarer. Hvis feilen vedvarer kan man ta kontakt med Register over reelle rettighetshavere |

## Ordliste

Definisjoner på begrep som er brukt i denne dokumentasjonen.

| Begrep                     | Definisjon                                                                                                                                        |
|:---------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------|
| API                        | Programmeringsgrensesnitt. Et grensesnitt i en programvare som gjør at spesifikke deler av denne kan aktiveres fra en annen programvare           |
| Tilgangsstyrt tjeneste/API | En tjeneste/API som krever autentisering/autorisering (for eksempel ved bruk av Maskinporten)                                                     |
| Reell rettighetshaver      | En reell rettighetshaver er en fysisk person som gjennom sin eierandel eller stemmeandel, alene eller sammen med andre, kontrollerer virksomheten |
| HTTP                       | Datakommunikasjonsstandard                                                                                                                        |
| HTTP-statuskoder           | Statuskoder for datakommunikasjonsstandard                                                                                                        |
| Request                    | Forespørsel mot et API. Dvs adressen til API'et samt eventuelle inputparametre                                                                    |
| Response                   | Data som returneres fra API'et etter at man har gjort en request/forespørsel                                                                      | 
| REST                       | Datakommunikasjonsmønster                                                                                                                         |
| JSON                       | Åpen standard for dataformat                                                                                                                      |
| Organisasjonsnummer        | Identifikasjonsnummer for virksomhet                                                                                                              |
| Fødselsnummer              | Identifikator for en person i Folkeregisteret. I våre API'er omfatter dette også D-nummer                                                         |
