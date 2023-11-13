---
title: Maskinporten
description: Veiledning for integrasjon mot Maskinporten
weight: 20
---
<!-- TOC -->
  * [Innledning](#innledning)
  * [Prosess for å ta i bruk våre APIer](#prosess-for-å-ta-i-bruk-våre-apier)
  * [Prosess for delegering av tilgang til en systemleverendør](#prosess-for-delegering-av-tilgang-til-en-systemleverendør)
    * [Bestilling fra systemleverandør](#bestilling-fra-systemleverandør)
    * [Innlesing i Altinns testmiljø - TT02](#innlesing-i-altinns-testmiljø---tt02)
    * [Hvordan delegerer jeg tilgang videre til systemleverandør?](#hvordan-delegerer-jeg-tilgang-videre-til-systemleverandør)
    * [Hvordan skal systemleverandør bruke den delegerte tilgangen?](#hvordan-skal-systemleverandør-bruke-den-delegerte-tilgangen)
  * [Hvordan teste et tilgangsstyrt API?](#hvordan-teste-et-tilgangsstyrt-api)
  * [Jeg har problemer med maskinport-integrasjonen eller delegering i Altinn](#jeg-har-problemer-med-maskinport-integrasjonen-eller-delegering-i-altinn)
<!-- TOC -->

## Innledning

Register over reelle rettighetshavere benytter maskinporten som autentiserings- og autorisasjonsmekanisme for
tilgangsstyrte tjenester. Maskinporten er en av Digdirs fellesløsninger og sørger for sikker autentisering og 
autorisasjon for datautveksling mellom virksomheter. Løsningen garanterer identiteten mellom virksomheter og gjør 
det mulig å binde sammen systemer og utvikle nye tjenester på en effektiv måte. Vi forutsetter at du i tillegg til å 
lese denne veiledningen setter deg grundig inn i Digdir sin egen dokumentasjon
om [maskinporten](https://samarbeid.digdir.no/maskinporten/maskinporten/25).

Hovedfokuset i denne 
dokumentasjonen er på maskinporten, men vi vil også beskrive hvordan du bruker Altinn for å delegere 
maskinporten-tilganger videre.

## Prosess for å ta i bruk våre APIer
Kall til APIene må inkludere et gyldig _token_ fra Maskinporten for å få tilgang. Under er prosessen for å få et slik 
token og benytte det mot våre API oppsummert:

1. Bestill og få tilgang til vår tjeneste i henhold til [bestillingsprosedyren](../).
    * Du vil motta et maskinporten-scope, og informasjon om hva det gir tilgang til. Det finnes to 
      mulige scope:
      * `brreg:reelle/offentlig`
      * `brreg:reelle/rapporteringspliktig`
2. Opprett en Maskinporten-integrasjon/klient
    * Dette innebærer at du har registrerer en klient hos maskinporten som knyttes opp mot det scopet du 
      har fått tildelt (se punkt 1).
    * Vi anbefaler at du følger den punktvise fremgangsmåten som beskrives i [Digdir sin dokumentasjon](https://samarbeid.digdir.no/maskinporten/konsument/119),
      samt [Maskinsportens guide til hvordan du bruker Maskinporten som API-konsument](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument)
3. Hent token fra maskinporten med klienten fra punkt 2.
   * Se [Digdirs dokumentasjon](https://docs.digdir.no/docs/Maskinporten/maskinporten_protocol_token)
4. Utfør kall mot vår tjeneste med token du fikk i punkt 3.
   * Tokenet skal inkluderes i `Authorization`-headeren slik: ```Authorization: Bearer  <access_token>```
   * Se [Digdirs sekvensdiagram](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument#5-be-om-token)
     for illustrasjon av hvordan dette fungerer.

___

## Prosess for delegering av tilgang til en systemleverendør
Delegering er relevant for virksomheter som ønsker å _delegere_ tilgang vidre til en leverandør. Denne prosessen 
forutsetter at virksomheten (ikke systemleverandøren) som skal ha tilgangen på forhånd har gjennomført
det som står under punkt 1 i forrige kapittel.

### Bestilling fra systemleverandør

Systemleverandører som har behov for å teste å hente data fra våre tjenester på vegne av et sett med kunder må få få delegert rettigheter i Altinns testmiljø TT02 på samme måte som de vil få delegert rettigheter i Produksjon.
Digdir har en nærmere beskrivelse av hvordan delegere, se [Digdir sin side om delegering via Altinn autorisasjon](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument.html#bruke-delegering-via-altinn-autorisasjon).  

Før delegering kan gjennomføres, og testing kan starte må systemleverandør sende en epost til opendata.rrh@brreg.no med
informasjon om følgende:

* Systemleverandørs organisasjonsnummer
* Systemleverandørs organisasjonsnavn
* Systemleverandørs kontaktpersons e-postadresse (som er tilknyttet testen)
* Systemleverandørs kontaktpersons mobiltelefonnummer (som er tilknyttet testen)
* Virksomheten som har tilgang sitt organisasjonsnummer
* Virksomheten som har tilgang sitt organisasjonsnavn
* Virksomheten som har tilgang sin kontaktpersons e-postadresse (som er tilknyttet testen)
* Virksomheten som har tilgang sin kontaktpersons mobiltelefonnummer (som er tilknyttet testen)

> **_NB!_** Samme informasjon må oppgis både for virksomheten med tilgang og systemleverandøren, siden begge
> virksomhetene må leses inn i TT02 for at det skal være mulig å gjennomføre en delegering i testmiljøet. En
> systemleverandør som leverer til flere virksomheter, trenger ikke melde inn alle virksomhetene for test, kun den som
> skal utføre delegeringen i test.

### Innlesing i Altinns testmiljø - TT02

Etter at vi har mottatt bestilling fra systemleverandør vil vi i samarbeid med Altinn sørge for at virksomhetene (den
som har fått tilgang samt systemeleverandør) blir lest inn i TT02 slik at det er mulig å gjennomføre delegeringen.  
Når det er gjort vil vi gi tilbakemelding om hvilket fødselsnummer som kan benyttes for innlogging i TT02.

Når innlesing i TT02 er gjennomført skal følgende være på plass:

* Virksomheten med rettigheter til tjenesten som skal testes er tilgjengelig i TT02
* Virksomheten er opprettet med en syntetisk person som det er mulig å logge inn i TT02 med
* Systemleverandøren som skal få delegert rettigheter for test er tilgjengelig i TT02

> **_NB!_** TT02 er et testmiljø med hovedsaklig syntetiske testdata, og innlesing av ekte virksomheter gjøres kun ved
> behov. Vær oppmerksom på at det da leses inn produksjonsdata om virksomheten i et testmiljø

### Hvordan delegerer jeg tilgang videre til systemleverandør?

Dersom din virksomhet har fått tilgang til våre tilgangsstyrte tjenester kan denne tilgangen delegeres videre til en
eller flere systemleverandører om ønskelig.  
Hvis delegeringen skal gjøres i Altinns testmiljø TT02 må systemleverandør først ha sendt en bestilling, og innlesing av
virksomheter i TT02 må være gjennomført (se over).

Delegering må gjøres i Altinn, og fremgangsmåte kan du finne
i [denne guiden](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument.html#bruke-delegering-via-altinn-autorisasjon).

Eksempel med skjermbilder for hvordan man praktisk gjør delegeringen kan du
finne [her](https://altinn.github.io/docs/utviklingsguider/api-delegering/tilgangsstyrer/).

Under "Legge til API-ressurser" må man søke opp og velge et delegeringsskjema som stemmer overens med det
maskinporten-scopet som virksomheten har fått.
Nedenfor viser vi hvilket scope som "matcher" hvilket delegeringsskjema:

Scope: brreg:reelle/offentlig  
Delegeringsskjema: "Register over reelle rettighetshavere - Offentlig myndighet - På vegne av"

Scope: brreg:reelle/rapporteringspliktig  
Delegeringsskjema: "Register over reelle rettighetshavere - Rapporteringspliktig virksomhet - På vegne av"

### Hvordan skal systemleverandør bruke den delegerte tilgangen?

Systemleverandør som skal bruke delegert tilgang kan
følge [denne guiden](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument.html#bruke-delegering-som-leverand%C3%B8r).

Det er verdt å poengtere enkelte ting knyttet til hvordan systemleverandør skal bruke delegert tilgang:

* Systemleverandør skal alltid bruke sin egen maskinporten-klient registrert med sitt eget virksomhetssertifikat ved
  henting av access-tokens fra maskinporten
* Systemleverandør må registrere det maskinporten-scopet de har fått delegert på sin egen maskinporten-klient
* Når du som systemleverandør skal hente et access-token fra maskinporten må du angi virksomhetens/konsumentens orgnr
  som consumer_org i JWT-grantet. Dette er orgnr på virksomheten som delegerte tilgangen. Maskinporten vil da sjekke i
  Altinn om et gyldig delegeringsforhold finnes mellom konsument og systemleverandør for aktuelt scope

___ 

## Hvordan teste et tilgangsstyrt API?

Før man har kommet så langt at man har laget en applikasjon som kan integrere seg mot våre tilgangsstyrte API'er ønsker
man gjerne å gjøre noen initielle tester.  
[Her er en how-to artikkel](https://docs.digdir.no/docs/idporten/oidc/oidc_sample_jwtgrant_postman) på hvordan du kan
bruke Postman for å teste API'er.

## Jeg har problemer med maskinport-integrasjonen eller delegering i Altinn

Hvis du har problemer med å ta i bruk maskinporten skal henvendelser i utgangspunktet gå til Digdir.  
Kontakt servicedesk@digdir.no oppgi client_id og miljø og forklar problemet.

Hvis du har problemer med å gjennomføre delegering av tilganger i Altinn-portalen skal henvendelser gå til
Altinn-servicedesk.  
Kontakt servicedesk@altinn.no, og forklar problemet.