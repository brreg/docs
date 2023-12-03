---
title: Tilgang for systemleverandører i test
description: Informasjon om hvordan en systemleverandør kan søke om tilgang til test
weight: 3
---

<!-- TOC -->
* [Innledning](#innledning)
  * [Tilgangsmuligheter for systemleverandører](#tilgangsmuligheter-for-systemleverandører)
    * [Opprettelse av fiktiv virksomhet](#opprettelse-av-fiktiv-virksomhet)
    * [Delegering fra eksisterende kunde](#delegering-fra-eksisterende-kunde)
  * [Hvordan bestiller jeg tilgang til tjenestene i test?](#hvordan-bestiller-jeg-tilgang-til-tjenestene-i-test)
  * [Hva gjør vi med bestillingen](#hva-gjør-vi-med-bestillingen)
<!-- TOC -->

{{< warning >}}
For øyeblikket er det kun mulig å søke om tilgang til våre APIer i testmiljøet. Tilgang til produksjonsmiljøet er foreløpig ikke åpent for eksterne brukere. Så snart dette er klart, vil vi informere om prosessen for å søke tilgang til produksjonsmiljøet. Vi vil gi informasjon så snart vi åpner opp for å bestille tilgang.
{{< /warning >}}

# Innledning
Hvis du er systemleverandør kan du få tilgang til vårt testmiljø.

**Hvis du har rett på direkte tilgang, [se egen side for direkte tilgang.](../tilgang-i-test)**

## Tilgangsmuligheter for systemleverandører

Som systemleverandør som ønsker å teste integrasjonen med våre tjenester, har du to hovedalternativer for å få delegert tilgang i Maskinporten i vårt testmiljø:

### Opprettelse av fiktiv virksomhet
Vi kan, etter forespørsel, opprette en fiktiv virksomhet i vårt testmiljø og delegere nødvendige tilganger til denne. Dette gir deg som systemleverandør muligheten til selv å delegere denne tilgangen videre til deg selv. Denne metoden er ideell for å teste funksjonaliteten uten å involvere en faktisk kunde.

### Delegering fra eksisterende kunde
Alternativt kan du be en av dine eksisterende kunder om å bestille tilgang i testmiljøet. Når kunden har mottatt tilgangen, kan de deretter delegere denne tilgangen til deg som systemleverandør.

## Hvordan bestiller jeg tilgang til tjenestene i test?
> **_NB!_** TT02 er et testmiljø med hovedsaklig syntetiske testdata, og innlesing av ekte virksomheter gjøres kun ved
> behov. Vær oppmerksom på at det da leses inn produksjonsdata om virksomheten i et testmiljø

Dersom du skal være systemleverandør sender du en epost til `opendata.rrh@brreg.no` hvor du
opplyser om følgende:

* Virksomhetens organisasjonsnummer
* Virksomhetens navn
* Navn, epost-adresse og telefonnummer for kontaktperson
* **Om dere ønsker opprettelse av en fiktiv virksomhet eller om dere får delegert tilgang via reell kunde**
  * Hvis en reell kunde skal delegere tilgang, må dere sende:
    * Kundens organisasjonsnummer
    * Kundens organisasjonsnavn
    * Kundens e-postadresse
    * Kundens mobiltelefonnummer

## Hva gjør vi med bestillingen
Etter at vi har mottatt bestilling fra systemleverandør vil vi i samarbeid med Altinn sørge for at virksomhetene (den som har fått tilgang samt systemeleverandør) blir lest inn i TT02 slik at det er mulig å gjennomføre delegeringen.
Når det er gjort vil vi gi tilbakemelding om hvilket fødselsnummer som kan benyttes for innlogging i TT02.

## Jeg har fått tilgang, hva gjør jeg nå?

Når du har fått en bekreftelse fra Brønnøysundregistrene om at du har fått tilgang til våre tjenester i vårt testmiljø vil neste steg
være å integrere seg mot Maskinporten. Vi har laget en [veiledning for
integrasjon mot maskinporten](../../maskinporten).