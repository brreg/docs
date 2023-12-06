---
title: Vanlig (direkte) tilgang
description: Informasjon om å søke om direkte tilgang til test
weight: 2
---

{{< warning >}}
For øyeblikket er det kun mulig å søke om tilgang til våre APIer i testmiljøet. Tilgang til produksjonsmiljøet er foreløpig ikke åpent for eksterne brukere. Så snart dette er klart, vil vi gi informasjon om prosessen for å søke tilgang til produksjonsmiljøet.
{{< /warning >}}

# Innledning
Hvis du har [rett på tilgang til våre tjenester](../hvem-kan-faa-tilgang) kan du bestille tilgang til vårt testmiljø. I vårt testmiljø kan du teste ut våre APIer med syntetiske data.

**Hvis du er systemleverandør, [se egen side for systemleverandører.](../systemleverandoerer)**


## Hvordan bestiller jeg tilgang til tjenestene i test?
Dersom du mener din virksomhet oppfyller kriteriene over sender du en epost til `opendata.rrh@brreg.no` hvor du
opplyser om følgende:

* Virksomhetens organisasjonsnummer
* Virksomhetens navn
* Navn, epost-adresse og telefonnummer for kontaktperson
* Hvilken hjemmel til utvidet tilgang virksomheten faller inn under (se over for informasjon om hvem som kan få tilgang)

## Hvordan delegere tilgang til en systemleverandør
> **_NB!_** Hvis delegeringen skal gjøres i Altinns testmiljø (TT02) må systemleverandør ha bestilt tilgang og ha enten:
> * Fått en fiktiv virksomhet med tilgang til vårt testmiljø.
> * En kunde som har fått tilgang og som kan delegere denne tilgangen til dere.

Dersom din virksomhet har fått tilgang til våre tilgangsstyrte tjenester kan denne tilgangen delegeres videre til en
eller flere systemleverandører om ønskelig.

Delegering må gjøres i Altinn, og fremgangsmåte kan du finne
i [denne guiden](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument.html#bruke-delegering-via-altinn-autorisasjon).

Eksempel med skjermbilder for hvordan man praktisk gjør delegeringen kan du
finne [her](https://altinn.github.io/docs/utviklingsguider/api-delegering/tilgangsstyrer/).

Under "Legge til API-ressurser" må man søke opp og velge et delegeringsskjema som stemmer overens med det
maskinporten-scopet som virksomheten har fått.
Nedenfor viser vi hvilket scope som "matcher" hvilket delegeringsskjema:

Scope: `brreg:reelle/offentlig`  
Delegeringsskjema: "Register over reelle rettighetshavere - Offentlig myndighet - På vegne av"

Scope: `brreg:reelle/rapporteringspliktig`  
Delegeringsskjema: "Register over reelle rettighetshavere - Rapporteringspliktig virksomhet - På vegne av"

### Jeg skal bruke en systemleverandør, hva gjør jeg?
Om du skal bruke en systemleverandør er det ikke sikkert at du trenger tilgang i vårt testmiljø. Hør med din leverandør om hvordan leverandøren ønsker å teste våre tjenester.  
Se mer på [egen side for bestilling for systemleverandører](../tilgang-for-systemleverandoerer-i-test).

## Jeg har tidligere bestilt tilgang, hva gjør jeg?
Dersom du tidligere har oversendt informasjonen over, trenger du ikke å gjøre noe. Vi vil ta kontakt dersom du må ettersende informasjon.

## Jeg har fått tilgang, hva gjør jeg nå?

Når du har fått en bekreftelse fra Brønnøysundregistrene om at du har fått tilgang til våre tjenester i vårt testmiljø vil neste steg
være å integrere seg mot Maskinporten. Vi har laget en [veiledning for
integrasjon mot maskinporten](../../maskinporten).
