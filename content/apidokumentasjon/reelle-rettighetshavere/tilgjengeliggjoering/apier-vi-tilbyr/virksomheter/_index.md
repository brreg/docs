---
title: Virksomheter
description: Beskrivelse av tjeneste for oppslag/søk i Register over reelle rettighetshavere
weight: 100
---

- [API-spesifikasjon](#api-spesifikasjon)
- [Kodeliste](#kodeliste)
- [Løsningsmodell](#løsningsmodell) 
- [Endringslogg](#endringslogg) 


`Virksomheter` er et API for oppslag/søk i Register over reelle rettighetshavere.

* APIet tilbyr opplysninger om registrerte virksomheter og deres reelle rettighetshavere ved oppslag med ulike
  parametere, samt nedlasting av registerets totalbestand
* APIet er tilgangsstyrt, se siden [Tilgang til APIer](../../tilgang-til-apier)
* Opplysningene om reelle rettighetshavere inkluderer fullt fødsels- eller D-nummer fra Folkeregisteret.
  APIet skjermer ikke opplysninger om mindreårige og andre som er unntatt fra innsyn

## API-spesifikasjon

APIet er tilgjengelig for konsumering gjennom Swagger-UI og som en nedlastbar OpenAPI-spesifikasjon. Her finner du
mer utfyllende informasjon om hva APIet tilbyr.

| Miljø      | Swagger-UI                           | OpenAPI-spesifikasjon                                    |
|------------|--------------------------------------|----------------------------------------------------------|
| Test       | https://rrh.ppe.brreg.no/api/oppslag | https://rrh.ppe.brreg.no/api/oppslag/openapi/openapi.zip |

## Kodeliste
Ved kall til våre API'er vil enkelte felter i responsene være kodeverdier.  
En kodeliste som inneholder alle relevante koder med beskrivelser kan du [laste ned her](rrh_kodeliste_virksomheter.xlsx).

## Løsningsmodell

Se løsningsmodell under informasjonsmodeller for [Virksomhet](../../../../../informasjonsmodeller/reelle-rettighetshavere/loesningsmodeller/virksomhet/rrh_loesningsmodell_virksomhet)

## Endringslogg

Endringsloggen dokumenterer alle endringer som er gjort på Virksomhet APIet for Reelle Rettighetshavere.  
Formatet er basert på [keep a changelog](https://keepachangelog.com/en/1.1.0/)
og dette prosjektet følger [semantisk versjonering](https://semver.org/spec/v2.0.0.html).

### 1.0.0-beta2 - 2024-02-28

#### Lagt til

- Nytt endepunkt for å hente en liste med alle tilgjenglige kodelister. Dette endepunktet kan feks. brukes til
  visning i eventuelle brukergrensesnitt, dynamisk oppdatering av kodelister, validering og lignende.

#### Endret

- Funksjonalitet for oppslag på virksomhet er endret til å inkludere opplysninger om både nåværende og tidligere registrerte reelle rettighetshavere.
- Søk på fødselsnummer er oppdatert til å gi en liste over virksomheter hvor personen, identifisert ved det angitte fødsels- eller D-nummeret, er eller har vært registrert som reell rettighetshaver.
