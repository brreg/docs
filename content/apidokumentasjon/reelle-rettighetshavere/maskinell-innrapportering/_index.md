---
title: Maskinell innrapportering
description: Beskrivelse av maskinell innrapportering for Register over reelle rettighetshavere
weight: 100
---

## Tilgang
For at ditt sluttbrukersystem skal kunne rapportere inn opplysninger om reelle rettighetshavere på vegne av en bruker trenger du en `api_klient` registert via Samarbeidsportalen/selvbetjening i DigDir.
* [Mer informasjon om tilgang finner du her](./hvordan-faa-tilgang)

## Innsending av opplysninger om reelle rettighetshavere
Ved å bruke APIet på vår Altinn 3-app kan et sluttbrukersystem sende inn opplysninger om reelle rettighetshavere på vegne av en bruker.
* [Mer informasjon om innsending av opplysninger finner du her](./hvordan-sende-inn)

## Eksempler
Opplysninger om Reelle rettighetshavere kan sendes inn på JSON-format. 
* [Eksempler på vanlige innrapporteringer kan du se her](./eksempler-paa-registrering)
* [Se også tekstlig beskrivelse av feltene i JSON-skjemaet](./beskrivelse-av-felter)
* JSON kan valideres mot [https://schema.brreg.no/reelle/altinn/schema.json](https://schema.brreg.no/reelle/altinn/schema.json)

### Test og produksjon
En detaljert beskrivelse av kravene til testing og oppstart i produksjon, finner du på [denne siden](./test-og-produksjon)