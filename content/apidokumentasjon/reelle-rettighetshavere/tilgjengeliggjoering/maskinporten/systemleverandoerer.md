---
title: Systemleverandører
description: Veiledning for integrasjon mot Maskinporten som systemleverandør
weight: 3
---

Veiledning for systemleverandører.

## Hvordan bestille tilgang som systemleverandør
{{< warning >}}
Systemleverandører kan ikke bestille tilgang i produksjon. I produksjon må tilgang delegeres av en aktør som vil være berettiget til å få tilgang til våre tjenester.
{{< /warning >}}
Gjelder det tilgang i test, må du se hvordan du kan bestille tilgang i vårt testmiljø på siden: [Bestille tilgang som systemleverandør](../../tilgang-til-apier/systemleverandoerer).

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

Systemleverandør som skal bruke delegert tilgang kan
følge [denne guiden](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument.html#bruke-delegering-som-leverand%C3%B8r).

## Prosess for å ta i bruk Maskinporten mot våre APIer
Kall til APIene må inkludere et gyldig _token_ fra Maskinporten for å få tilgang. For å hente ut et gyldig token kan du følge disse stegene:

1. Opprett en Maskinporten-integrasjon/klient
   * Dette innebærer at du som systemleverandør har bestilt din egen maskinporten-klient som er registrert med sitt eget virksomhetssertifikat ved
     henting av access-tokens fra maskinporten
   * Systemleverandør må registrere det maskinporten-scopet de har fått delegert på sin egen maskinporten-klient
   * Vi anbefaler at du følger den punktvise fremgangsmåten som beskrives i [Digdir sin dokumentasjon](https://samarbeid.digdir.no/maskinporten/konsument/119),
     samt [Maskinportens guide til hvordan du bruker Maskinporten som API-konsument](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument)
2. Hent token fra maskinporten med klienten fra punkt 2.
   * Når du som systemleverandør skal hente et access-token fra maskinporten må du angi virksomhetens/konsumentens orgnr
     som consumer_org i JWT-grantet. Dette er orgnr på virksomheten som delegerte tilgangen. Maskinporten vil da sjekke i
     Altinn om et gyldig delegeringsforhold finnes mellom konsument og systemleverandør for aktuelt scope
   * Se [Digdirs dokumentasjon](https://docs.digdir.no/docs/Maskinporten/maskinporten_protocol_token)
   * Se [denne guiden for hvordan du kan hente ut et maskinporten-token](https://docs.digdir.no/docs/idporten/oidc/oidc_sample_jwtgrant_postman)
3. Utfør kall mot vår tjeneste med token du fikk i punkt 3.
    * Tokenet skal inkluderes i `Authorization`-headeren slik: ```Authorization: Bearer  <access_token>```
    * Se [Digdirs sekvensdiagram](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument#5-be-om-token)
      for illustrasjon av hvordan dette fungerer.
    * Se [denne guiden for hvordan du kan bruke et maskinporten-token mot et API](https://docs.digdir.no/docs/idporten/oidc/oidc_sample_jwtgrant_postman)

> Vi validerer ikke at Audience (Aud-feltet) i token er satt

## Jeg har problemer med maskinport-integrasjonen eller delegering i Altinn

Hvis du har problemer med å ta i bruk maskinporten skal henvendelser i utgangspunktet gå til Digdir.  
Kontakt `servicedesk@digdir.no` oppgi client_id og miljø og forklar problemet.

Hvis du har problemer med å gjennomføre delegering av tilganger i Altinn-portalen skal henvendelser gå til
Altinn-servicedesk.  
Kontakt `servicedesk@altinn.no`, og forklar problemet.