---
title: Informasjonsmodeller
description: Beskrivelser av informasjonsmodeller
weight: 100
alwaysopen: true
---

En informasjonsmodell er en formell beskrivelse av en begrenset mengde av informasjon innenfor et gitt domene eller interesseområde. For å beskrive et domene, benyttes to modelltyper - forretningsobjektmodell og strukturmodell.

I undersidene finner du forretningsobjektmodeller og strukturmodeller delt inn etter register eller fagområde. Løsningsmodellene finner du under de enkelte API-beskrivelsene.
[Link til informasjonsmodeller i GitHub](https://github.com/brreg/informasjonsmodeller)


### Forretningsobjektmodell

En forretningsobjektmodell beskriver de viktigste forretningsobjektene innenfor et forretningsdomene.

Et forretningsobjekt kan anses som en representasjon av et begrep som brukes i et bestemt forretningsdomene og som omfatter en avgrenset informasjonsmengde eller informasjonsenhet.  Forretningsobjekter kan ha ulik størrelse og oppløsning. Eksempler er person, virksomhet, støtteordning, søknad eller ektepakt.  Forretningsobjekter kan ha relasjoner til hverandre, som beskriver hvordan de forholder seg til eller roller de har overfor hverandre innenfor et forretningsdomene.

Forretningsobjektmodeller er nyttige hjelpemiddel når man skal etablere en felles, faglig forståelse av et forretningsdomene og enes om et omforent begrepsapparat. De benyttes også som utgangspunkt for å lage strukturmodeller.



### Strukturmodeller

En strukturmodell beskriver detaljert hvilken informasjon som inngår i et forretningsdomene og hvordan de er logisk relatert, uavhengig av teknologi og implementasjon. I modellen struktureres informasjonen i henhold til tenkte enheter – typer eller sett av objekter eller entiteter som omtales som klasser. Klassene kan være konkrete eller abstrakte, som f.eks. Person og Adresse. Typen av kunnskap eller informasjon om disse typene av objekter, beskrives som egenskaper ved klassene. En egenskap ved klassen Person, kan f.eks. være fødselsnummer eller navn. I strukturmodellen beskriver man også relasjonene mellom klassene og hvilke roller de har overfor hverandre, som f.eks. at en person kan ha en adresse.

Når man lager strukturmodeller, tar man utgangspunkt i forretningsobjektmodellen som er laget for tilsvarende domene. Forretningsobjektene og relasjonene som er definert mellom dem kan bidra til å avdekke hva som er hensiktmessige klasser og relasjoner. Strukturmodellene skal være mest mulig uavhengige av kontekst og egne seg for gjenbruk. De skal også bidra til lik organisering av data innenfor og på tvers av interesseområder uavhengig av teknologivalg.



### Løsningsmodell

En løsningsmodell er en logisk modell som beskriver hvordan informasjonen struktureres og brukes i en konkret løsning, som f.eks. i et API eller en database. Løsningsmodellene er laget med utgangspunkt i innholdet i en eller flere strukturmodeller. Mens strukturmodellene er generelle og skal kunne gjenbrukes i flere løsninger, er løsningsmodellen laget for en gitt løsning. Normalt vil elementene i en løsningsmodell være en delmengde av elementene i en eller flere strukturmodeller.
