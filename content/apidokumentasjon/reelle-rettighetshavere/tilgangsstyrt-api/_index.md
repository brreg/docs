---
title: Tilgangsstyrt API
description: Beskrivelse av tilgangsstyrt API for Register over reelle rettighetshavere
weight: 100
---

## Innledning
Brønnøysundregistrene tilbyr et tilgangsstyrt, standardisert maskin-til-maskin-tjeneste (API) som kan benyttes av eksterne konsumenter for innsyn i Register over reelle rettighetshavere.

Denne dokumentasjonen viser hvordan eksterne systemer kan integrere seg mot APIet, og hvordan man benytter seg av tjenesten for å hente data.


***Denne siden er fortsatt under utvikling.***

## API-referanse
Denne tjenesten tilbyr informasjon om reelle rettighetshavere ved oppslag på organisasjonsnummer, inklusive fødselsnummer eller D-nummer.
Tjenesten skjermer ikke informasjon om mindreårige og andre som er unntatt fra innsyn.

***OpenAPI-spesifikasjon kommer snart, vi jobber med å finpusse responsmodellen***

***Lenker til Swagger-dokumentasjon kommer her.***


## Hvordan få tilgang

For å få tilgang til APIet må du sende e-post til `opendata.rrh@brreg.no`. I e-posten må du opplyse om hvilket organisasjonsnummer det gjelder, og hvilken hjemmel til utvidet tilgang virksomheten faller inn under.  
Hvis tilgangen gjelder testmiljø må du i tillegg oppgi hvilken ip-adresse dere kommer fra da API'ene i test har ip-filtrering.  
Vi trenger også kontaktperson, med navn, epost-adresse og telefonnummer.

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
Konsumenter må autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_guide_apikonsument.html).

For å kunne få tilgang til APIet er det tre forutsetninger.

1. Virksomhetssertifikat
2. Registrert klient hos Maskinporten
3. I dialogen med Brønnøysundregistrene om å få tilgang til API'et vil din virksomhet ha fått informasjon om hvilket av de to scopene virksomheten har fått tilgang til:
JWT-token fra Maskinporten mot ett av disse scopene:
   1. `brreg:reelle/offentlig`
   2. `brreg:reelle/rapporteringspliktig`

Tokenet som hentes fra Maskinporten må bli sendt som autorisasjonstoken (Bearer token) når et kall mot tjenesten blir utført.

Se [veiledning for integrasjon mot Maskinporten]({{<ref "mp-integrasjonsveiledning.md">}}).

[Regelverk](https://lovdata.no/dokument/SF/forskrift/2021-06-21-2056?q=forskrift%20reelle%20rettighetshavere): Hjemler for tilgjengeliggjøring av data fra Brønnøysundregistrene.
## Grensesnittbeskrivelse

| HTTP-metode | URL                                                       | Beskrivelse                                                                                                                                                                                      |
|:------------|:----------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GET         | https://\{domene\}/api/virksomheter/{organisasjonsnummer} | Hent opplysninger om reelle rettighetshavere for en virksomhet                                                                                                                                   |
| GET         | https://\{domene\}/api/virksomheter/json                  | Hent totalbestand over alle reelle rettighetshavere som er registrert i register over reelle rettighetshavere. Returneres i JSON-format i en ZIP-fil. Responsen inneholder ikke historiske data. |

**Domener**:

* For testmiljø : `https://rrh.ppe.brreg.no`
* For produksjon: `https://rrh.brreg.no`

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer. Forespørselen valideres og returnerer opplysninger om reelle rettighetshavere, inklusive fødselsnummer og d-nummer, på oppgitt organisasjonsnummer.

### Testdata
Se [underside for testdata]({{<ref "testdata_for_tilgangsstyrt_api.md">}}). Her finner du organisasjonsnummer du kan bruke bruke i vårt testmiljø og hvilke data du får i retur.

#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.  
#### Versjonering

**Vi anbefaler at dere legger til header `Accept` med verdi `application/vnd.brreg.reelle.virksomheter.v1+json;charset=UTF-8`.**  
**Om vi kommer med en ny versjon av APIet vil dere da være sikre på at dere får den forespurte versjonen tilbake.**


#### Validering

* Forespørselen skal alltid inneholde organisasjonsnummeret det gjøres oppslag på.
* Dersom forespørselen inneholder et organisasjonsnummer som ikke er lovlig oppbygd, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 samt et dokument (på JSON-format) i retur. JSON-dokumentet inneholder opplysninger om reelle rettighetshavere.


##### Eksempelrespons for oppslag på organisasjonsnummer
***Eksempelrespons for oppslag på organisasjonsnummer kommer snart, vi jobber med å finpusse responsmodellen***

### Totalbestand

#### Beskrivelse

Henter ut alle gjeldende opplysninger i registeret i form av JSON i en ZIP-fil. Filene blir oppdatert en gang i døgnet.

#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.

#### Response

Dersom kallet lykkes får man HTTP-status 200 samt en Zippet fil (på JSON-format) i retur. Filen inneholder alle gjeldende opplysninger i Register over reelle rettighetshavere.  
**I vårt testmiljø kan filen inneholde flere elementer en de som er beskrevet på vår side om [testdata]({{<ref "testdata_for_tilgangsstyrt_api.md">}}).** 

#### Eksempelrespons for totalbestand
***Eksempelfil for oppslag på totalbestand kommer snart, vi jobber med å finpusse responsmodellen***

---\0+\


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

| Begrep                | Definisjon                                                                                                                                        |
|:----------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------|
| API                   | Programmeringsgrensesnitt                                                                                                                         |
| Tilgangsstyrt API     | Et API som krever autentisering/autorisering (for eksempel ved bruk av Maskinporten)                                                              |
| Reell rettighetshaver | En reell rettighetshaver er en fysisk person som gjennom sin eierandel eller stemmeandel, alene eller sammen med andre, kontrollerer virksomheten |
| HTTP                  | Datakommunikasjonsstandard                                                                                                                        |
| HTTP-statuskoder      | Statuskoder for datakommunikasjonsstandard                                                                                                        |
| REST                  | Datakommunikasjonmønster                                                                                                                          |
| JSON                  | Åpen standard for dataformat                                                                                                                      |
| Organisasjonsnummer   | Identifikasjonsnummer for virksomhet                                                                                                              |

---
