---
title: Tilgang
description: Beskrivelse av hvordan man får tilgang til å sende inn registreringer som tredjeleverandør.
weight: 1
---

For å kunne rapportere inn opplysninger om Reelle rettighetshavere på vegne av dine kunder gjennom APIet til vår Altinn 3-app kan du følge guiden på denne siden.

> **_NB!_** Hvis du som systemleverandør har gjort dette tidligere i forbindelse med en annen integrasjon mot 
> Altinn 3-apper trenger du sannsynligvis ikke å gjøre det på nytt. Du kan da gjenbruke API-klienten du tidligere har opprettet, 
> forutsatt at API-klienten har tilgang til scopene `altinn:instances.read` og `altinn:instances.write`.  

## 1. Generell informasjon om hvordan sluttbrukersystem kan autentisere brukere via ID-porten
Se [denne dokumentasjonen](https://docs.altinn.studio/nb/api/authentication/id-porten/) for å få en grunnleggende forståelse av hvordan sluttbrukersystem kan autentisere brukere via ID-porten, og dermed kunne benytte API for vår Altinn 3-app.

## 2. Registrere systemleverandør som API-konsument i maskinporten
Hvis du er en systemleverandør som tidligere ikke har integrert deg mot Altinn 3-apper kan du følge [DigDirs guide for å registrere deg som API-konsument i maskinporten](https://samarbeid.digdir.no/maskinporten/konsument/119).\
Dette vil gi deg tilgang til Samarbeidsportalen, noe som igjen gir deg tilgang til å opprette API-klienter gjennom Selvbetjeningsløsningen.

## 3. Opprette en API-klient
En API-klient opprettes ved å sette opp en integrasjon av typen `api_klient`. Vi anbefaler at du gjør det gjennom Digdirs Selvbetjeningsløsning eller Selvbetjenings-API.\
For mer informasjon, [se Digdirs guide: Registrering av klienter](https://docs.digdir.no/docs/idporten/oidc/oidc_func_clientreg), eller se nedenfor hvordan du gjør det gjennom DigDirs Selvbetjeningsløsning:

1. Logg på [Samarbeidsportalen](https://minside-samarbeid.digdir.no/my-organisation/integrations/admin)
   1. Opprett ny Integrasjon
2. Fyll ut integrasjonsdata:
   * [**Se denne PDFen**](Sette%20opp%20api_client%20i%20ID-porten.pdf) for et eksempel på en `api_klient` i test-miljø
     * NB! Pass på å velge følgende scopes: `altinn:instances.read` og `altinn:instances.write`
     * Når sluttbruker har logget inn gjennom ID-porten, må sluttbruker sendes tilbake til en gyldig `redirect-uri`. Denne eksempel-klienten har konfigurert følgende gyldige `redirect uri`-er for å forenkle testing:
       * https://test.superbrasluttbrukersystem.no/reelle/innrapportering - For å kunne sende brukere tilbake til tjeneste i testmiljø
       * https://oauth.pstmn.io/v1/callback - For å teste innlogging og innsending gjennom Postman må man kunne sendes tilbake til Postman
       * http://localhost:8080/reelle/innrapportering - For at utviklere skal skal kunne teste lokalt må man kunne sendes tilbake til localhost

Når API-klienten er opprettet er forutsetningene på plass for at du kan sende inn skjema på vegne av en bruker. [Se detaljer om innsendingsprosessen her.](../hvordan-sende-inn)


## Jeg har problemer
Hvis du har problemer med å registrere en `api_klient` via Selvbetjeningsløsningen skal henvendelser i utgangspunktet gå til Digdir.
Kontakt servicedesk@digdir.no oppgi client_id og miljø og forklar problemet.
