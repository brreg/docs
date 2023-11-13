---
title: APIer vi tilbyr
description: Beskrivelse av APIer som tilbys
weight: 1
---

Se undersidene i menyen til venstre for hvilke APIer som tilbys.

## Versjonering

APIene følger Semantic Versioning (SemVer) standarden, der major/hovedversjonen er en del av URLen til tjenesten.
URLer er tilgjengelig på følgende format: `https://rrh.brreg.no/api/domene/v{hovedversjon}/{tjeneste}`.

* Eventuelle inkompatible endringer vil medføre en ny hovedversjon, og dermed en ny URL
* Ved publisering av en ny hovedversjon vil også den forrige hovedversjonen være operativ i en overgangsperiode
* Eksempel på endring som medfører ny hovedversjon:
    * Fjerne eller endre navn på et attributt i en HTTP-respons
    * Fjerne eller endre navn på et REST-endepunkt eller dets parameter
* Eksempel på endringen som _ikke_ medfører ny hovedversjon
    * Legge til et attributt i en HTTP-respons
    * Legge til et endepunkt eller legge til et frivilig parameter på eksisterende endepunkt

## Varsling om endringer

Ved utgivelse av en ny hovedversjon vil brukere bli varslet. Dette varselet vil inneholde informasjon om den
kommende endringen, en overgangsperiode og relevant dokumentasjon for å hjelpe brukere med å tilpasse seg endringene.

Vi vil legge ut varsel/driftsmeldinger i god tid på brreg.no.
Se her for flere detaljer om hvilke [kanaler vi bruker for å informere våre brukere](../nyheter-og-driftsmeldinger).
