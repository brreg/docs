---
title: Virksomheter
description: Beskrivelse av tjeneste for oppslag/søk i Register over reelle rettighetshavere
weight: 100
---

- [API-spesifikasjon](#api-spesifikasjon)
- [Løsningsmodell](#løsningsmodell) 
- [Endringer i APIet](#endringer-i-apiet) 


`Virksomheter` er et API for oppslag/søk i Register over reelle rettighetshavere. 
* APIet tilbyr
  * Opplysninger om registrerte virksomheter og deres reelle rettighetshavere
  * Nedlasting av totalbestand på json-format
  * Endringslogg: Dette brukes typisk for å fange opp at det har skjedd endringer på registreringer om reelle rettighetshavere i registeret
  * Kodelister: Kan brukes til visning i eventuelle brukergrensesnitt, dynamisk oppdatering av kodelister, validering og lignende. Endepunktet er åpent, og krever ikke maskinporten-autentisering
* Alle endepunktene i APIet med unntak av Kodelister er tilgangsstyrt, se [Tilgang til endepunkter](#tilgang-til-endepunkter)

## API-spesifikasjon

APIet er tilgjengelig for konsumering gjennom Swagger-UI og som en nedlastbar OpenAPI-spesifikasjon. Her finner du
mer utfyllende informasjon om hva APIet tilbyr.

| Miljø      | Swagger-UI                           | OpenAPI-spesifikasjon                                    |
|------------|--------------------------------------|----------------------------------------------------------|
| Test       | https://rrh.ppe.brreg.no/api/oppslag | https://rrh.ppe.brreg.no/api/oppslag/openapi/openapi.zip |
| Produksjon | https://rrh.brreg.no/api/oppslag     | https://rrh.brreg.no/api/oppslag/openapi/openapi.zip     |

## Løsningsmodell

Se løsningsmodell under informasjonsmodeller for [Virksomhet](../../../../../informasjonsmodeller/reelle-rettighetshavere/loesningsmodeller/virksomhet/rrh_loesningsmodell_virksomhet)

## Tilgang til endepunkter
Vi tilbyr ulike [maskinporten-scopes](../../maskinporten/hvordan-bruke-maskinporten) til forskjellige aktører. Tabellen under beskriver hvilke endepunkter maskinporten-scopene har tilgang til. Alle endepunktene i APIet med unntak av Kodelister er tilgangsstyrt, se tabellen under for å finne ut hva ditt
maskinporten-scope har tilgang til.

| Aktør                                                                                                | Maskinporten-scope                                                                                                | Kodelister | Oppslag på virksomhetens organisasjonsnummer | Oppslag på fødselsnummer eller D-nummer | Nedlasting av totalbestand | Endringslogg |
|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|------------|----------------------------------------------|-----------------------------------------|----------------------------|--------------|
| Offentlig myndighet i § 3-11 (1)                                                                     | **brreg:reelle/offentlig**                                                                                        | X          | X                                            | X                                       | X                          | X            |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav a, b, c, e, g, h til k, n og o | **brreg:reelle/rapporteringspliktig**                                                                             | X          | X                                            |                                         |                            |              |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav d, f, l og m                   | **brreg:reelle/rapporteringspliktig.begrenset**                                                                   | X          | X                                            |                                         |                            |              |
| Medier, sivilsamfunnsorganisasjoner og høyere utdanningsinstitusjoner i § 3-11 (2), (3) og (4) ledd. | **brreg:reelle/media**, **brreg:reelle/sivilsamfunnsorganisasjon**, **brreg:reelle/hoeyereutdanningsinstitusjon** | X          | X                                            |                                         |                            |              |                          
| Alle andre                                                                                           | **Krever ikke maskinporten-scope**                                                                                | X          |                                              |                                         |                            |              |

## Tilgang til informasjon som er begrenset

Se tabellen under for å finne ut om ditt maskinporten-scope har tilgang til å se fødselsnummer og D-Nummer. Full oversikt over alle tilgjengelige
felter og særregler kan ses i løsningsmodell for [virksomhet](../../../../../informasjonsmodeller/reelle-rettighetshavere/loesningsmodeller/virksomhet/rrh_loesningsmodell_virksomhet).

| Aktør                                                                                                | Maskinporten-scope                                                                                                | Fødselsnummer og D-nummer |  
|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|---------------------------|
| Offentlig myndighet i § 3-11 (1)                                                                     | **brreg:reelle/offentlig**                                                                                        | X                         |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav a, b, c, e, g, h til k, n og o | **brreg:reelle/rapporteringspliktig**                                                                             | X                         |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav d, f, l og m                   | **brreg:reelle/rapporteringspliktig.begrenset**                                                                   | X                         
| Medier, sivilsamfunnsorganisasjoner og høyere utdanningsinstitusjoner i § 3-11 (2), (3) og (4) ledd. | **brreg:reelle/media**, **brreg:reelle/sivilsamfunnsorganisasjon**, **brreg:reelle/hoeyereutdanningsinstitusjon** |                           |

## Endringer i APIet

Her dokumenteres alle endringer som er gjort på Virksomhet APIet for Reelle Rettighetshavere.  
Formatet er basert på [keep a changelog](https://keepachangelog.com/en/1.1.0/)
og dette prosjektet følger [semantisk versjonering](https://semver.org/spec/v2.0.0.html).

### 1.2.0 - 2025-03-06

#### Lagt til
* Registreringer kan nå inneholde objektet `uoverensstemmelse`. 
  * Se løsningsmodellen for mer informasjon om objektet

### 1.1.0 - 2024-10-24

#### Lagt til
* Språkstøtte for kodelisteverdier
  * Det er introdusert et nytt parameter som muliggjør uthenting av responser med kodelisteverdier også på nynorsk og engelsk.
  * Funksjonaliteten er implementert på følgende endepunkter: `hentRegistreringspliktigVirksomhet`, `finnRegistreringspliktigeVirksomheter`, `hentRelevanteKodelister`
  * Funksjonaliteten er implementert i form av en frivillig HTTP-header: `Accept-Language`. Mulige verdier for headeren: `nob` (bokmål), `nno` (nynorsk) og `eng` (engelsk)
  * Hvis `Accept-Language`-headeren ikke er spesifisert eller er spesifisert med en ugyldig verdi, vil responsen returnere verdier på Bokmål som standard.

### 1.0.0 - 2024-09-28
API-ene er ikke lenger i beta-fasen og kan nå anses som stabile.

### 1.0.0-beta2 - 2024-02-28

#### Lagt til

- Nytt endepunkt for å hente en liste med alle tilgjenglige kodelister. Dette endepunktet kan feks. brukes til
  visning i eventuelle brukergrensesnitt, dynamisk oppdatering av kodelister, validering og lignende.

#### Endret

- Funksjonalitet for oppslag på virksomhet er endret til å inkludere opplysninger om både nåværende og tidligere registrerte reelle rettighetshavere.
- Søk på fødselsnummer er oppdatert til å gi en liste over virksomheter hvor personen, identifisert ved det angitte fødsels- eller D-nummeret, er eller har vært registrert som reell rettighetshaver.
