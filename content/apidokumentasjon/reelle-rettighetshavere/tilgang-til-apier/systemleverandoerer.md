---
title: Systemleverandører
description: Informasjon om hvordan en systemleverandør kan søke om tilgang til test
weight: 3
---

{{< warning >}}
For øyeblikket er det kun mulig å søke om tilgang til våre APIer i testmiljøet. Tilgang til produksjonsmiljøet er foreløpig ikke åpent for eksterne brukere. Så snart dette er klart, vil vi gi informasjon om prosessen for å søke tilgang til produksjonsmiljøet.
{{< /warning >}}

Hvis du er systemleverandør kan du få tilgang til vårt testmiljø.

**Hvis du har rett på direkte tilgang, [se egen side for direkte tilgang.](../vanlig-direkte-tilgang)**

## Tilgangsmuligheter for systemleverandører

Systemleverandører må få delegert tilgang i Maskinporten for å få tilgang i vårt testmiljø. **Her har du to alternativer:**

### 1) Opprettelse av fiktiv virksomhet
Vi kan, etter forespørsel, opprette en fiktiv virksomhet i vårt testmiljø og tildele et maskinporten-scope til denne. Dette gir deg som systemleverandør muligheten til selv å delegere denne tilgangen videre til deg selv. Denne metoden er ideell for å teste funksjonaliteten uten å involvere en faktisk kunde.

**Prosessen for å bestille tilgang og få opprettet en fiktiv virksomhet er:**
1. Send en epost til `opendata.rrh@brreg.no` hvor du opplyser om følgende:
   * Virksomhetens organisasjonsnummer
   * Virksomhetens navn
   * Navn på deres kontaktperson (som er involvert i testen)
   * Epost-adresse til deres kontaktperson (som er involvert i testen)
   * Telefonnummer til deres kontaktperson (som er involvert i testen)
   * **Si at dere ønsker å delegere tilgang selv via en fiktiv virksomhet**
2. Vi mottar bestillingen og gjør følgende:
   * Leser inn ditt virksomhets organisasjonsnummer i Altinns testmiljø (TT02)
   * Oppretter en fiktiv virksomhet som dere kan logge på med et fiktivt fødselsnummer
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
3. Du som systemleverandør sender en epost til `opendata.rrh@brreg.no` hvor du opplyser om følgende:
    * Virksomhetens organisasjonsnummer
    * Virksomhetens navn
    * Navn på deres kontaktperson (som er involvert i testen)
    * Epost-adresse til deres kontaktperson (som er involvert i testen)
    * Telefonnummer til deres kontaktperson (som er involvert i testen)
    * Kundens organisasjonsnummer
    * Kundens organisasjonsnavn
    * Navn på kundens kontaktperson (som er involvert i testen)
    * Epost-adresse til kundens kontaktperson (som er involvert i testen)
    * Telefonnummer til kundens kontaktperson (som er involvert i testen)
4. Vi mottar bestillingen og gjør følgende:
    * Leser inn ditt og deres kundes organisasjonsnummer i Altinns testmiljø (TT02)
    * Oppretter en fiktiv person med et fiktivt fødselsnummer for deres kunde sin virksomhet
    * Oppretter en fiktiv person med et fiktivt fødselsnummer for deres virksomhet
    * Sender mail til dere med informasjonen over
5. Når dere har mottatt bekreftelse fra oss om at alt er klart kan du:
    * Be din kunde om å delegere tilgang fra sin virksomheten til deres virksomhet i Altinn.
    * Se mer om dette på [side om Maskinporten for systemleverandører](../../maskinporten/systemleverandoerer)

## Jeg har fått tilgang, hva gjør jeg nå?

Når du har fått tilgang til våre tjenester i testmiljøet vil neste steg
være å integrere seg mot Maskinporten. Vi har laget en [veiledning for
integrasjon mot maskinporten](../../maskinporten/hvordan-bruke-maskinporten-som-systemleverandør).