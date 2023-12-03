---
title: Hvordan bruke Maskinporten
description: Veiledning for integrasjon mot Maskinporten for direkte tilgang
weight: 1
---

<!-- TOC -->
  * [Innledning](#innledning)
  * [Prosess for å ta i bruk våre APIer](#prosess-for-å-ta-i-bruk-våre-apier)
  * [Hvordan teste et tilgangsstyrt API?](#hvordan-teste-et-tilgangsstyrt-api)
  * [Jeg har problemer med maskinport-integrasjonen eller delegering i Altinn](#jeg-har-problemer-med-maskinport-integrasjonen-eller-delegering-i-altinn)
<!-- TOC -->

## Innledning
> **_NB!_** Hvis du er systemleverandør eller skal bruke systemleverandør, se [egen side for bruk av maskinporten som systemleverandør](../hvordan-bruke-maskinporten-som-systemleverandør).

**Vi forutsetter at du i tillegg til å
lese denne veiledningen setter deg grundig inn i [Digdir sin egen dokumentasjon
om maskinporten](https://samarbeid.digdir.no/maskinporten/maskinporten/25).**

## Prosess for å ta i bruk våre APIer
Kall til APIene må inkludere et gyldig _token_ fra Maskinporten for å få tilgang. Under er prosessen for å få et slik
token og benytte det mot våre API oppsummert:

1. Bestill og få tilgang til vår tjeneste i henhold til [bestillingsprosedyren for tilgang](../../tilgang-til-apier/tilgang-i-test).
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

## Hvordan teste et tilgangsstyrt API?
[Her er en how-to artikkel](https://docs.digdir.no/docs/idporten/oidc/oidc_sample_jwtgrant_postman) på hvordan du kan
bruke Postman for å teste API'er.

## Jeg har problemer med maskinport-integrasjonen eller delegering i Altinn

Hvis du har problemer med å ta i bruk maskinporten skal henvendelser i utgangspunktet gå til Digdir.  
Kontakt `servicedesk@digdir.no` oppgi client_id og miljø og forklar problemet.

Hvis du har problemer med å gjennomføre delegering av tilganger i Altinn-portalen skal henvendelser gå til
Altinn-servicedesk.  
Kontakt `servicedesk@altinn.no`, og forklar problemet.