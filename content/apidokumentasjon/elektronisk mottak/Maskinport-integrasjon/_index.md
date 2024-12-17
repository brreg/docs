---
title: Integrasjon direkte mot BR
description: Beskrivelser av API innen BRs elektroniske mottak av meldinger
weight: 100
---

## Innledning

Brønnøysundregistrenes elektroniske mottak har et REST-grensesnitt som kan benyttes av eksterne parter for innsending av meldinger.

## Sikkerhetsmekanismer

Siden dette er begrensede API så skal kallende parter autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_overordnet.html).

For å kunne få tilgang til våre begrensede APIer må man bruke et JWT-token fra Maskinporten med scopet `brreg:mottak`

Access-tokenet oppgis i headeren `Authorization`. Husk `Bearer` før tokenet.

| Header        | Verdi                       |
|---------------|-----------------------------|
| Authorization | Bearer <maskinporten-token> |
