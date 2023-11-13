---
title: Maskinporten
description: Veiledning for integrasjon mot Maskinporten
weight: 20
---


## Innledning

Register over reelle rettighetshavere benytter maskinporten som autentiserings- og autorisasjonsmekanisme for tilgangsstyrte tjenester.  
Maskinporten er en av Digdirs fellesløsninger og sørger for sikker autentisering og autorisasjon for datautveksling mellom virksomheter.  
Løsningen garanterer identiteten mellom virksomheter og gjør det mulig å binde sammen systemer og utvikle nye tjenester på en effektiv måte.  
Vi forutsetter at du i tillegg til å lese denne veiledningen grundig setter deg inn i Digdir sin egen dokumentasjon om [maskinporten](https://samarbeid.digdir.no/maskinporten/maskinporten/25).  
Selv om hovedfokuset i denne dokumentasjonen er på maskinporten vil vi også beskrive hvordan du bruker Altinn for å delegere maskinporten-tilganger videre. 

## Prosess for å ta i bruk våre tilgangsstyrte tjenester

Dette kapitlet oppsummerer i korte trekk hva du som virksomhet må gjøre for å komme til det punktet at du faktisk kan gjøre et oppslag mot våre tilgangsstyrte tjenester.  
NB! Hvis du skal delegere tilgang videre til en systemleverandør trenger du bare å utføre det som står under punkt 1. Deretter må systemleverandør følge prosessen for systemleverandører nedenfor.  
Før du kan benytte tjenestene er det tre forutsetninger som må være på plass:

1. Du må ha bestilt og fått tilgang til tjenesten i henhold til bestillingsprosedyre [her]({{<ref "./_index.md#hvordan-bestiller-jeg-tilgang-til-tjenester">}}). Du vil deretter ha mottatt informasjon om hvilket maskinporten-scope din virksomhet har fått tilgang til. Foreløpig er det disse scopene som er aktuelle:
    * `brreg:reelle/offentlig`
    * `brreg:reelle/rapporteringspliktig`
2. Du må ha skaffet et virksomhetssertifikat knyttet til organisasjonsnummeret for din virksomhet, ett for test og ett for produksjon.
    * Sjekk [denne siden](https://docs.digdir.no/docs/Maskinporten/maskinporten_virksomhetssertifikat#hvem-kan-utstede-virksomhetssertifikater) for informasjon om hvilke sertifikatutstedere som er godkjent til utsteding av virksomhetssertifikater i Norge
    * Når det gjelder test må virksomheten anskaffe et testsertifikat utstedt under en egen test-CA slik at sertifikatene ikke aksepteres av systemer og løsninger som aksepterer skarpe sertifikater. 
3. Du må ta i bruk maskinporten som API-konsument. Dette betyr blant annet at du har registrert en klient hos maskinporten som knyttes opp mot det scopet du har fått tildelt (se punkt 1).  
Vi anbefaler at du følger den punktvise fremgangsmåten som beskrives i [Digdir sin dokumentasjon](https://samarbeid.digdir.no/maskinporten/konsument/119).  
Du bør i tillegg se på [denne mer detaljerte dokumentasjonen](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument) om hvordan man bruker maskinporten som API-konsument.

Når disse forutsetningene er på plass vil du kunne gjøre et API-kall mot maskinporten for å [hente et access-token](https://docs.digdir.no/docs/Maskinporten/maskinporten_protocol_token) for det scopet du har fått tilgang til.  
Tokenet må deretter sendes som autorisasjonstoken (Bearer token) når et kall mot tjenesten blir utført.
[Dette sekvensdiagrammet](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument#5-be-om-token) illustrerer på en enkel måte hvordan dette fungerer.  

## Prosess for delegering slik at systemleverandør kan benytte våre tilgangsstyrte tjenester

Denne prosessen forutsetter at virksomheten (ikke systemleverandøren) som skal ha tilgangen på forhånd har gjennomført det som står under punkt 1 i forrige kapittel.

### Bestilling fra systemleverandør

Systemleverandører som har behov for å teste å hente data fra våre tjenester på vegne av et sett med kunder må få få delegert rettigheter i Altinns testmiljø TT02 på samme måte som de vil få delegert rettigheter i Produksjon.
Digdir har en nærmere beskrivelse av hvordan delegere, se [Digdir sin side om delegering via Altinn autorisasjon](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument.html#bruke-delegering-via-altinn-autorisasjon).  

Før delegering kan gjennomføres, og testing kan starte må systemleverandør sende en epost til opendata.rrh@brreg.no med informasjon om følgende:
* Systemleverandørs organisasjonsnummer
* Systemleverandørs organisasjonsnavn
* Systemleverandørs kontaktpersons e-postadresse (som er tilknyttet testen)
* Systemleverandørs kontaktpersons mobiltelefonnummer (som er tilknyttet testen)
* Virksomheten som har tilgang sitt organisasjonsnummer
* Virksomheten som har tilgang sitt organisasjonsnavn
* Virksomheten som har tilgang sin kontaktpersons e-postadresse (som er tilknyttet testen)
* Virksomheten som har tilgang sin kontaktpersons mobiltelefonnummer (som er tilknyttet testen)
* Hvis tilgangen gjelder testmiljø må systemleverandør i tillegg oppgi hvilken ip-adresse de kommer fra da tjenestene i test har ip-filtrering
> **_NB!_** Samme informasjon må oppgis både for virksomheten med tilgang og systemleverandøren, siden begge virksomhetene må leses inn i TT02 for at det skal være mulig å gjennomføre en delegering i testmiljøet. En systemleverandør som leverer til flere virksomheter, trenger ikke melde inn alle virksomhetene for test, kun den som skal utføre delegeringen i test.

### Innlesing i Altinns testmiljø - TT02
Etter at vi har mottatt bestilling fra systemleverandør vil vi i samarbeid med Altinn sørge for at virksomhetene (den som har fått tilgang samt systemeleverandør) blir lest inn i TT02 slik at det er mulig å gjennomføre delegeringen.  
Når det er gjort vil vi gi tilbakemelding om hvilket fødselsnummer som kan benyttes for innlogging i TT02.

Når innlesing i TT02 er gjennomført skal følgende være på plass:
* Virksomheten med rettigheter til tjenesten som skal testes er tilgjengelig i TT02
* Virksomheten er opprettet med en syntetisk person som det er mulig å logge inn i TT02 med
* Systemleverandøren som skal få delegert rettigheter for test er tilgjengelig i TT02
> **_NB!_** TT02 er et testmiljø med hovedsaklig syntetiske testdata, og innlesing av ekte virksomheter gjøres kun ved behov. Vær oppmerksom på at det da leses inn produksjonsdata om virksomheten i et testmiljø


### Hvordan delegerer jeg tilgang videre til systemleverandør?
Dersom din virksomhet har fått tilgang til våre tilgangsstyrte tjenester kan denne tilgangen delegeres videre til en eller flere systemleverandører om ønskelig.  
Hvis delegeringen skal gjøres i Altinns testmiljø TT02 må systemleverandør først ha sendt en bestilling, og innlesing av virksomheter i TT02 må være gjennomført (se over).

Delegering må gjøres i Altinn, og fremgangsmåte kan du finne i [denne guiden](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument.html#bruke-delegering-via-altinn-autorisasjon).

Eksempel med skjermbilder for hvordan man praktisk gjør delegeringen kan du finne [her](https://altinn.github.io/docs/utviklingsguider/api-delegering/tilgangsstyrer/).

Under "Legge til API-ressurser" må man søke opp og velge et delegeringsskjema som stemmer overens med det maskinporten-scopet som virksomheten har fått.
Nedenfor viser vi hvilket scope som "matcher" hvilket delegeringsskjema:

Scope: brreg:reelle/offentlig  
Delegeringsskjema: "Register over reelle rettighetshavere - Offentlig myndighet - På vegne av"

Scope: brreg:reelle/rapporteringspliktig  
Delegeringsskjema: "Register over reelle rettighetshavere - Rapporteringspliktig virksomhet - På vegne av"

### Hvordan skal systemleverandør bruke den delegerte tilgangen?

Systemleverandør som skal bruke delegert tilgang kan følge [denne guiden](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument.html#bruke-delegering-som-leverand%C3%B8r).  

Det er verdt å poengtere enkelte ting knyttet til hvordan systemleverandør skal bruke delegert tilgang:
  * Systemleverandør skal alltid bruke sin egen maskinporten-klient registrert med sitt eget virksomhetssertifikat ved henting av access-tokens fra maskinporten
  * Systemleverandør må registrere det maskinporten-scopet de har fått delegert på sin egen maskinporten-klient
  * Når du som systemleverandør skal hente et access-token fra maskinporten må du angi virksomhetens/konsumentens orgnr som consumer_org i JWT-grantet. Dette er orgnr på virksomheten som delegerte tilgangen. Maskinporten vil da sjekke i Altinn om et gyldig delegeringsforhold finnes mellom konsument og systemleverandør for aktuelt scope

## Hvordan teste et tilgangsstyrt API?
Før man har kommet så langt at man har laget en applikasjon som kan integrere seg mot våre tilgangsstyrte API'er ønsker man gjerne å gjøre noen initielle tester.  
[Her er en how-to artikkel](https://docs.digdir.no/docs/idporten/oidc/oidc_sample_jwtgrant_postman) på hvordan du kan bruke Postman for å teste API'er.


## Jeg har problemer med maskinport-integrasjonen eller delegering i Altinn
Hvis du har problemer med å ta i bruk maskinporten skal henvendelser i utgangspunktet gå til Digdir.  
Kontakt servicedesk@digdir.no oppgi client_id og miljø og forklar problemet.  

Hvis du har problemer med å gjennomføre delegering av tilganger i Altinn-portalen skal henvendelser gå til Altinn-servicedesk.  
Kontakt servicedesk@altinn.no, og forklar problemet.