---
title: Hvordan bruke Maskinporten
description: Veiledning for integrasjon mot Maskinporten for direkte tilgang
weight: 1
---

## Innledning
> **_NB!_** Hvis du er systemleverandør eller skal bruke systemleverandør, se [egen side for bruk av maskinporten som systemleverandør](../systemleverandoerer).

**Vi forutsetter at du i tillegg til å
lese denne veiledningen setter deg grundig inn i [Digdir sin egen dokumentasjon
om maskinporten](https://samarbeid.digdir.no/maskinporten/maskinporten/25).**

## Prosess for å ta i bruk Maskinporten mot våre APIer
Kall til APIene må inkludere et gyldig _token_ fra Maskinporten for å få tilgang. For å hente ut et gyldig token kan du følge disse stegene:

1. Bestill og få tilgang til vår tjeneste i henhold til [bestillingsprosedyren for tilgang](../../tilgang-til-apier/vanlig-direkte-tilgang).
    * Du vil motta et maskinporten-scope, og informasjon om hva det gir tilgang til. Det finnes to
      mulige scope:
        * `brreg:reelle/offentlig`
        * `brreg:reelle/rapporteringspliktig`
2. Opprett en Maskinporten-integrasjon/klient
    * Dette innebærer at du har registrert en klient hos maskinporten som knyttes opp mot det scopet du
      har fått tildelt (se punkt 1).
    * Vi anbefaler at du følger den punktvise fremgangsmåten som beskrives i [Digdir sin dokumentasjon](https://samarbeid.digdir.no/maskinporten/konsument/119),
      samt [Maskinportens guide til hvordan du bruker Maskinporten som API-konsument](https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument)
3. Hent token fra maskinporten med klienten fra punkt 2.
    * Se [Digdirs dokumentasjon](https://docs.digdir.no/docs/Maskinporten/maskinporten_protocol_token)
    * Se [denne guiden for hvordan du kan hente ut et maskinporten-token](https://docs.digdir.no/docs/idporten/oidc/oidc_sample_jwtgrant_postman)
4. Utfør kall mot vår tjeneste med token du fikk i punkt 3.
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