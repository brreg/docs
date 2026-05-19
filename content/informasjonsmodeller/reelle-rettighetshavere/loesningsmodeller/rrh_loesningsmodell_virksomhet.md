---
title: Virksomhet
description: Løsningsmodell for tilgjengeliggjøring i Register over reelle rettighetshavere.
weight: 10
---

{{% children description="true" /%}}

![Tilgangsstyrt API løsningsmodell](https://github.com/brreg/informasjonsmodeller/blob/main/registeroverreellerettighetshavere/loesningsmodeller/løsningsmodell_api_virksomheter.png?raw=true)

Feltbeskrivelser for løsningsmodellen finner du i [swagger-dokumentasjonen til applikasjonen](https://rrh.brreg.no/api/oppslag/v1/docs/feltbeskrivelser.html).

## Særregler for personer unntatt innsyn

For personer unntatt innsyn, fjernes følgende data på reell rettighetshaver:

* Navn
* Fødselsdato
* Fødselsnummer/D-nummer
* Grunnlagstype
* Mellomliggende virksomhet

Se mer info
i [forskrift til lov om register over reelle rettighetshavere](https://lovdata.no/forskrift/2021-06-21-2056/§3-9).
