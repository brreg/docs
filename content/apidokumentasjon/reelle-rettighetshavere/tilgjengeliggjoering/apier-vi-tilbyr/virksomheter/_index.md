---
title: Virksomheter
description: Beskrivelse av tjeneste for oppslag/søk i Register over reelle rettighetshavere
weight: 100
---

- [API-spesifikasjon](#api-spesifikasjon)
- [Løsningsmodell](#løsningsmodell) 
- [Endringer i APIet](#endringer-i-apiet) 


`Virksomheter` er et API for oppslag/søk i Register over reelle rettighetshavere. Hvilke endepunkt og informasjon du kan få tilgang til kan du lese mer om på [denne siden](../../tilgang-til-apier/hvem-kan-faa-tilgang-til-hva).

## API-spesifikasjon

APIet er tilgjengelig for konsumering gjennom Swagger-UI og som en nedlastbar OpenAPI-spesifikasjon. Her finner du
mer utfyllende informasjon om hva APIet tilbyr.

| Miljø      | Swagger-UI                           | OpenAPI-spesifikasjon                                    |
|------------|--------------------------------------|----------------------------------------------------------|
| Test       | https://rrh.ppe.brreg.no/api/oppslag | https://rrh.ppe.brreg.no/api/oppslag/openapi/openapi.zip |
| Produksjon | https://rrh.brreg.no/api/oppslag     | https://rrh.brreg.no/api/oppslag/openapi/openapi.zip     |

## Løsningsmodell

Se løsningsmodell under informasjonsmodeller for [Virksomhet](../../../../../informasjonsmodeller/reelle-rettighetshavere/loesningsmodeller/virksomhet/rrh_loesningsmodell_virksomhet)

## Endringer i APIet

Her dokumenteres alle endringer som er gjort på Virksomhet APIet for Reelle Rettighetshavere.  
Formatet er basert på [keep a changelog](https://keepachangelog.com/en/1.1.0/)
og dette prosjektet følger [semantisk versjonering](https://semver.org/spec/v2.0.0.html).

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
