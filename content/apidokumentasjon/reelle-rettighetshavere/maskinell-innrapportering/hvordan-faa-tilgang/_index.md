---
title: Tilgang
description: Beskrivelse av hvordan man får tilgang til å sende inn registreringer som tredjeleverandør.
weight: 10
---

For å kunne rapportere inn reelle rettighetshavere på vegne av dine kunder kan du følge guiden på denne siden:
<!-- TOC -->
  * [1. Sette opp api_klient hos ID-porten](#1-sette-opp-api_klient-hos-id-porten)
    * [Sette opp api_klient via Selvbetjening på Samarbeidsportalen](#sette-opp-api_klient-via-selvbetjening-på-samarbeidsportalen)
  * [2. Registrere datasystem og signere egenerklæring hos Altinn](#2-registrere-datasystem-og-signere-egenerklæring-hos-altinn)
  * [3. Bestille tilgang til Altinns REST API](#3-bestille-tilgang-til-altinns-rest-api)
  * [Jeg har problemer](#jeg-har-problemer)
<!-- TOC -->

> **_NB!_** Hvis du som sluttbrukersystem har gjort dette tidligere i forbindelse med en annen integrasjon mot ID-porten og Altinn så trenger du **_ikke_** å gjøre det på nytt. Du kan da gjenbruke API-nøkkelen du fikk fra Altinn, og `api_klient`-en du opprettet hos ID-porten. API-klienten må ha tilgang til scopene `altinn:instances.read` og `altinn:instances.write`.  


## 1. Sette opp api_klient hos ID-porten

For å lage en integrasjon av typen `api_klient` hos ID-porten anbefaler vi at du gjør det gjennom Digdirs Selvbetjening eller Selvbetjenings-API.
For mer informasjon, [se Digdirs guide: Registrering av klienter](https://docs.digdir.no/docs/idporten/oidc/oidc_func_clientreg), eller se neste kapittel.

### Sette opp api_klient via Selvbetjening på Samarbeidsportalen

For å sette opp en `api_klient` gjennom Selvbetjeningsløsningen hos Digdir kan du gjøre følgende:

1. Logg på [Samarbeidsportalen](https://minside-samarbeid.digdir.no/my-organisation/integrations/admin)
   1. Opprett ny Integrasjon
2. Fyll ut integrasjonsdata.
   * [**Se denne PDFen**](Sette%20opp%20api_client%20i%20ID-porten.pdf) for et eksempel på en `api_klient` i test-miljø.
     * Når sluttbruker har logget inn gjennom ID-porten, må sluttbruker sendes tilbake til en gyldig `redirect-uri`. Denne eksempel-klienten har konfigurert følgende gyldige `redirect uri`-er for å forenkle testing:
       * https://test.superbrasluttbrukersystem.no/reelle/innrapportering - For å kunne sende brukere tilbake til tjeneste i testmiljø.
       * https://oauth.pstmn.io/v1/callback - For å teste innlogging og innsending gjennom Postman må man kunne sendes tilbake til Postman.
       * http://localhost:8080/reelle/innrapportering - For at utviklere skal skal kunne teste lokalt må man kunne sendes tilbake til localhost
   * `api_klient` må ha tilgang til scopene `altinn:instances.read` og `altinn:instances.write`
     * **_NB_** Hvis du ikke kan gi deg selv disse scopene må du først registrere ditt datasystem hos Altinn og bestille tilgang til Altinns REST API. Se hvordan i neste kapittel.

## 2. Registrere datasystem og signere egenerklæring hos Altinn

For å få lov til å integrere et datasystem mot Altinn må du registrere ditt system hos Altinn.
Dette gjør du ved å:
1. Gjøre som beskrevet i Steg 1. i [Digdirs guide.](https://altinn.github.io/docs/api/datasystem/)

## 3. Bestille tilgang til Altinns REST API
Innrapportering gjøres ved API-kall mot vår Altinn APP. For å få lov til dette trenger du tilgang til Altinns REST API.
Som du også kan lese i [Digdirs guide](https://altinn.github.io/docs/api/datasystem/) kan dette gjøres på [denne lenken.](https://digdir.apps.altinn.no/digdir/be-om-api-nokkel/)
* [**Se denne PDFen**](Bestill%20tilgang%20til%20REST%20API%20-%20Digitaliseringsdirektoratet.pdf) for å se et eksempel på hva du trenger å fylle ut. 

Når du har fått tilgang til Altinns REST API skal du:
   * Motta en API-nøkkel. Denne må legges ved alle REST-kall mot Altinn APPen
   * Få lov til å gi `api_klient`-en du opprettet hos ID-porten tilgang til scopene `altinn:instances.read` og `altinn:instances.write`.
      * Dette kan du gjøre ved å logge på [Samarbeidsportalen](https://minside-samarbeid.digdir.no/my-organisation/integrations/admin), velg `api_klient`-en du opprettet i listen over integrasjoner, og legg til scopene til klienten.


## Jeg har problemer
Hvis du har problemer med å registrere en `api_klient` hos ID-porten skal henvendelser i utgangspunktet gå til Digdir.
Kontakt servicedesk@digdir.no oppgi client_id og miljø og forklar problemet.

Hvis du har problemer med å registrere ditt datasystem hos Altinn eller problemer med å bestille tilgang til Altinns REST API-portalen skal henvendelser gå til Altinn-servicedesk.
Kontakt servicedesk@altinn.no, og forklar problemet.

