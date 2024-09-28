---
title: Systemleverandører
description: Informasjon om hvordan en systemleverandør kan søke om tilgang til test
weight: 3
---

Hvis du er systemleverandør kan du få tilgang til vårt testmiljø.

**Hvis du har rett på direkte tilgang, [se egen side for direkte tilgang.](../vanlig-direkte-tilgang)**

## Tilgangsmuligheter for systemleverandører i vårt testmiljø

Systemleverandører må få delegert tilgang i Maskinporten for å få tilgang i vårt testmiljø. **Her har du to alternativer:**

### 1) Delegering fra fiktiv kunde
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
   * Se mer om dette på [side om Maskinporten for systemleverandører](../../maskinporten/systemleverandoerer)
   

### 2) Delegering fra eksisterende kunde
Alternativt kan dere be en av dine eksisterende kunder om å bestille tilgang i testmiljøet. Når kunden har mottatt tilgangen, kan de deretter delegere denne tilgangen til deg som systemleverandør.  

**Prosessen for å få delegert tilgang i vårt testmiljø blir da:**
1. Kunden som skal delegere tilgang til din virksomhet bestiller direkte tilgang:
   * Se hvordan dette gjøres på [side for å bestille vanlig (direkte) tilgang](../vanlig-direkte-tilgang)
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
    * Leser inn systemleverandørs organisasjonsnummer i Altinns testmiljø (TT02)
    * Leser inn kundens organisasjonsnummer i Altinns testmiljø (TT02)
    * **NB! Vær oppmerksom på at vi her leser inn produksjonsdata om virksomhetene i et testmiljø**
    * Oppretter en fiktiv person med et fiktivt fødselsnummer for kunden sin virksomhet i TT02
    * Sender mail til dere med informasjonen over
5. Når dere har mottatt bekreftelse fra oss om at alt er klart kan du som systemleverandør:
    * Be din kunde om å logge på med den fiktive personen i Altinn TT02, og delegere tilgang fra sin virksomhet til deres virksomhet i Altinn
    * Be din kunde om å oppgi hvilket scope de har fått tildelt da du som systemleverandør må vite dette når du skal hente maskinporten-token
    * Se mer om dette på [side om Maskinporten for systemleverandører](../../maskinporten/systemleverandoerer)

## Jeg har fått tilgang, hva gjør jeg nå?

Når du har fått tilgang til våre tjenester vil neste steg
være å integrere seg mot Maskinporten. Vi har laget en [veiledning for
integrasjon mot maskinporten](../../maskinporten/systemleverandoerer).