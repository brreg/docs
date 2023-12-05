---
title: Systemleverandører
description: Informasjon om hvordan en systemleverandør kan søke om tilgang til test
weight: 3
---

{{< warning >}}
For øyeblikket er det kun mulig å søke om tilgang til våre APIer i testmiljøet. Tilgang til produksjonsmiljøet er foreløpig ikke åpent for eksterne brukere. Så snart dette er klart, vil vi gi informasjon om prosessen for å søke tilgang til produksjonsmiljøet.
{{< /warning >}}

# Innledning
Hvis du er systemleverandør kan du få tilgang til vårt testmiljø.

**Hvis du har rett på direkte tilgang, [se egen side for direkte tilgang.](../tilgang-i-test)**

## Tilgangsmuligheter for systemleverandører

Systemleverandører må få delegert tilgang i Maskinporten for å få tilgang i vårt testmiljø. **Her har du to alternativer:**

### 1) Opprettelse av fiktiv virksomhet
Vi kan, etter forespørsel, opprette en fiktiv virksomhet i vårt testmiljø og tildele et maskinporten-scope til denne. Dette gir deg som systemleverandør muligheten til selv å delegere denne tilgangen videre til deg selv. Denne metoden er ideell for å teste funksjonaliteten uten å involvere en faktisk kunde.

### 2) Delegering fra eksisterende kunde
Alternativt kan du be en av dine eksisterende kunder om å bestille tilgang i testmiljøet. Når kunden har mottatt tilgangen, kan de deretter delegere denne tilgangen til deg som systemleverandør.

## Hvordan bestiller jeg tilgang til tjenestene i test?
Dersom du skal være systemleverandør sender du en epost til `opendata.rrh@brreg.no` hvor du
opplyser om følgende:

* Virksomhetens organisasjonsnummer
* Virksomhetens navn
* Navn, epost-adresse og telefonnummer for kontaktperson (som er involvert i testen)
* **Om dere ønsker opprettelse av en fiktiv virksomhet eller om dere får delegert tilgang via reell kunde**
  * Hvis en reell kunde skal delegere tilgang, må dere sende:
    * Kundens organisasjonsnummer
    * Kundens organisasjonsnavn
    * Kundens e-postadresse (som er involvert i testen)
    * Kundens mobiltelefonnummer (som er involvert i testen)

## Hva gjør vi med bestillingen
Etter at vi har mottatt bestillingen vil vi sørge for at din virksomhet blir lest inn i Altinns testmiljø (TT02). Det vil da være mulig å få delegert tilgang.
Dersom du valgte delegering via en fiktiv virksomhet vil vi gi informasjon om hvilket fødselsnummer som kan benyttes for innlogging i Altinns testmiljø (TT02).

## Jeg har fått tilgang, hva gjør jeg nå?

Når du har fått tilgang til våre tjenester i testmiljøet vil neste steg
være å integrere seg mot Maskinporten. Vi har laget en [veiledning for
integrasjon mot maskinporten](../../maskinporten/hvordan-bruke-maskinporten-som-systemleverandør).