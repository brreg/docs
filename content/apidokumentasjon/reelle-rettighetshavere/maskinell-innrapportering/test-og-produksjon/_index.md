---
title: Test og produksjon
description: Beskrivelse av hvordan systemleverandørene skal gjennomføre testing før de tar i bruk løsningen i produksjon
weight: 5
---

Vi forventer at systemleverandørene setter seg grundig inn i vår implementasjonsguide før de tar i bruk løsningen i test og etter hvert i produksjon.

## Krav til testgjennomføring
Systemleverandørene har ansvar for egen testgjennomføring. Det må fokuseres på at alle API-kallene mot vår app (preutfylling, validering, innsending etc) fungerer som forventet. Vi vil bistå med testdata, feilsøk, eventuell feilretting samt oppfølging av skjema som er sendt inn i testmiljøet.

## Testmiljø og testdata
* Systemleverandørene må forholde seg til at det kun skal brukes syntetiske data i test.
* Under testingen må systemleverandør bruke syntetiske testbrukere og virksomheter fra [Tenor Testdatasøk](https://www.skatteetaten.no/skjema/testdata/), eventuelt ta kontakt med oss hvis dere er usikre på hvilke testdata dere kan benytte. Se underkapitlet "Tenor Testdatasøk" for detaljer om hvordan dere kan finne testdata.

### Tenor Testdatasøk
Slik kan du bruke Tenor Testdatasøk for å finne testdata:
* Logg deg inn i [Tenor Testdatasøk](https://www.skatteetaten.no/skjema/testdata/). Denne krever innlogging med ID-porten, så her må du logge deg inn med din personlige bruker.
* Klikk på "Virksomhet". Når du går inn på en virksomhet kan du klikke på "Kildedata". Her kan du feks finne fødselsnummer for daglig leder (DAGL) eller styreleder (LEDE) som dere kan benytte til pålogging via ID-porten i sluttbrukersystemet.
* Når du finner en virksomhet du ønsker å teste med er det viktig å verifisere at virksomheten har en organisasjonsform som er registreringsplitkig i registeret. I tillegg må du finne en rolleinnehaver for virksomheten som har en rolle som gjør at vedkommende har lov til å fylle ut og sende inn skjemaet.
  * Følgende organisasjonsformer er registreringspliktige: AS, ASA, SE, ESEK, ANS, DA, BA, PRE, EOFG, KS, SA, BBL, BRL, SPA, PK, GFS, NUF, STI, FLI
  * Følgende roller for virksomheten har lov til å fylle ut og sende inn skjema: INNH, MEDL, LEDE, NEST, DAGL, DTPR, DTSO, KOMP, FFØR, REPR, KONT, KNUF. I sluttbrukersystemet må du altså logge på via ID-Porten med en person som har en av disse rollene.

## Oppsummering av test og oppstart i produksjon
Systemleverandørene skal etter avsluttet testperiode og i forkant av produksjonssetting oppsummere testen. Oppsummeringen skal vise hva som er testet, samt status etter gjennomført test inkludert oversikt over feil og mangler. Systemleverandørene skal på Brønnøysundregistrenes forespørsel kunne fremlegge dokumentasjon på hvordan integrasjonen er testet.

## Testmiljø og produksjonsmiljø
For mer teknisk informasjon om testmiljø og produksjonsmiljø samt hvordan du sender inn skjema maskinelt kan du se på [denne siden](../hvordan-sende-inn)
