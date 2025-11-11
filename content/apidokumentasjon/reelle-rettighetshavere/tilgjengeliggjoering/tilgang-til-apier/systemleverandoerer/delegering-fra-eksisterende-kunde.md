---
title: Delegering fra eksisterende kunde
description: Hvordan systemleverandører kan få delegert tilgang fra en eksisterende kunde
weight: 100
---

Be en av dine eksisterende kunder om å bestille tilgang i testmiljøet. Når kunden har mottatt tilgangen, kan de deretter delegere denne tilgangen til deg som systemleverandør.

**Prosessen for å få delegert tilgang i vårt test- og produksjonsmiljø blir da:**
1. Kunden som skal delegere tilgang til din virksomhet bestiller direkte tilgang:
   * Se hvordan dette gjøres på [side for å bestille vanlig (direkte) tilgang](../../vanlig-direkte-tilgang)
2. Kunden får bekreftelse om at de har fått tilgang
3. Du som systemleverandør sender en epost til `opendata@brreg.no` hvor du opplyser om følgende:
    * Systemleverandørs organisasjonsnummer
    * Systemleverandørs navn
    * Kontaktinformasjon til systemleverandørs kontaktperson for test (testansvarlig)
      * Navn til testansvarlig
      * Epost-adresse til testansvarlig
      * Telefonnummer til testansvarlig
    * Kundens organisasjonsnummer
    * Kundens navn
    * Kontaktinformasjon til kunden sin kontaktperson for test (testansvarlig)
      * Navn til testansvarlig
      * Epost-adresse til testansvarlig
      * Telefonnummer til testansvarlig
4. Vi mottar bestillingen og gjør følgende:
    * For testmiljø (TT02)
      * Leser inn systemleverandørs organisasjonsnummer i Altinns testmiljø (TT02)
      * Leser inn kundens organisasjonsnummer i Altinns testmiljø (TT02)
      * **NB! Vær oppmerksom på at vi her leser inn produksjonsdata om virksomhetene i et testmiljø**
      * Oppretter en fiktiv person med et fiktivt fødselsnummer for kunden sin virksomhet i TT02 
      * Sender mail til dere med informasjonen over
   * For produksjonsmiljø
     * Steget er ikke relevant for produksjonsmiljøet
5. Når dere har mottatt bekreftelse fra oss om at alt er klart kan du som systemleverandør:
   * For testmiljø (TT02)
       * Be din kunde om å logge på med den fiktive personen i Altinn TT02, og delegere tilgang fra sin virksomhet til deres virksomhet i Altinn
   * For produksjonsmiljø
     * Be din kunde om å delegere tilgang fra sin virksomhet til deres virksomhet i Altinn
   * Be din kunde om å oppgi hvilket scope de har fått tildelt da du som systemleverandør må vite dette når du skal hente maskinporten-token
   * Se mer om dette på [side om Maskinporten for systemleverandører](../../../maskinporten/systemleverandoerer)