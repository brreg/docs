---
title: Delegering fra fiktiv kunde
description: Hvordan systemleverandører kan teste ved å delegere tilgang fra en fiktiv kunde
weight: 100
---

{{< warning >}}
Fiktiv virksomhet kan kun brukes i testmiljøet. I produksjon må du ha en reell kunde som delegerer tilgangen til deg som systemleverandør.
{{< /warning >}}

Vi kan etter forespørsel opprette en fiktiv virksomhet som simulerer en kunde i vårt testmiljø, og tildele et maskinporten-scope til denne. Dette gir deg som systemleverandør muligheten til selv å delegere denne tilgangen videre til deg selv. Denne metoden er ideell for å teste funksjonaliteten uten å involvere en faktisk kunde.

**Prosessen for å bestille tilgang og få opprettet en fiktiv virksomhet er:**
1. Du som systemleverandør sender en epost til `opendata@brreg.no` hvor du opplyser om følgende:
   * Systemleverandørs organisasjonsnummer
   * Systemleverandørs navn
   * Kontaktinformasjon til deres kontaktperson for test (testansvarlig)
     * Navn til testansvarlig
     * Epost-adresse til testansvarlig
     * Telefonnummer til testansvarlig
   * **Skriv at dere ønsker å delegere tilgang selv via en fiktiv virksomhet**
2. Vi mottar bestillingen og gjør følgende:
   * Leser inn din virksomhets organisasjonsnummer i Altinns testmiljø (TT02). Vær oppmerksom på at vi her leser inn produksjonsdata om din virksomhet i et testmiljø
   * Oppretter en fiktiv virksomhet som dere kan logge på med et fiktivt fødselsnummer
   * Tildeler et maskinporten-scope til den fiktive virksomheten
   * Sender mail til dere med informasjonen over
3. Når dere har mottatt bekreftelse fra oss om at alt er klart kan dere:
   * Delegere tilgang fra den fiktive virksomheten til deres virksomhet i Altinn
   * Se mer om dette på [side om Maskinporten for systemleverandører](../../../maskinporten/systemleverandoerer)
