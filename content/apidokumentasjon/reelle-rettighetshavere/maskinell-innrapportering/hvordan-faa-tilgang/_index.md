---
title: Tilgang
description: Beskrivelse av hvordan man får tilgang til å sende inn registreringer som systemleverandør.
weight: 1
---

For å kunne rapportere inn opplysninger om reelle rettighetshavere på vegne av dine kunder gjennom APIet til vår Altinn 3-app kan du følge guiden på denne siden.

> **_NB!_** Hvis du som systemleverandør har gjort dette tidligere i forbindelse med en annen integrasjon mot 
> Maskinporten og/eller ID-Porten trenger du sannsynligvis ikke å gjøre det på nytt. Du kan da gjenbruke API-klienten du tidligere har opprettet, 
> forutsatt at API-klienten har tilgang til scopene `openid`, `altinn:instances.read` og `altinn:instances.write`.  

> **_NB!_** Maskinell innrapportering for Reelle rettighetshavere krever at sluttbrukeren er logget inn via ID-Porten.
> Dette betyr at [Altinn 2 Virksomhetsbrukere](https://altinn.github.io/docs/api/rest/kom-i-gang/virksomhetsbrukere/)
> og [Altinn 3 Systembruker](https://docs.altinn.studio/nb/authentication/what-do-you-get/systemuser/) IKKE støttes.

## 1. Generell informasjon om hvordan sluttbrukersystem kan autentisere brukere via ID-porten
Se [denne dokumentasjonen](https://docs.altinn.studio/nb/api/authentication/id-porten/) for å få en grunnleggende forståelse av hvordan sluttbrukersystem kan autentisere brukere via ID-porten, og dermed kunne benytte API for vår Altinn 3-app.

## 2. Registrere systemleverandør som API-konsument
Hvis du er en systemleverandør som tidligere ikke har integrert deg mot Maskinporten og/eller ID-Porten kan du følge [DigDirs guide for å registrere deg som API-konsument](https://samarbeid.digdir.no/maskinporten/konsument/119).\
Opplys i forespørselen til DigDir at du skal benytte Brønnøysundregistrenes lovpålagte API for innrapportering av opplysninger om reelle rettighetshavere til Register over reelle rettighetshavere.\
Dette vil gi deg tilgang til Samarbeidsportalen, noe som igjen gir deg tilgang til å opprette API-klienter gjennom Selvbetjeningsløsningen.

## 3. Opprette en API-klient
En API-klient opprettes ved å sette opp en integrasjon av typen `api_klient`. Vi anbefaler at du gjør det gjennom Digdirs Selvbetjeningsløsning eller Selvbetjenings-API.\
For mer informasjon, [se Digdirs guide: Registrering av klienter](https://docs.digdir.no/docs/idporten/oidc/oidc_func_clientreg), eller se nedenfor hvordan du gjør det gjennom DigDirs Selvbetjeningsløsning:

1. Logg på [Samarbeidsportalen](https://minside-samarbeid.digdir.no/my-organisation/integrations/admin)
   1. Opprett ny Integrasjon
2. Fyll ut integrasjonsdata:
   * [**Se denne PDFen**](opprett_api_klient.pdf) for et eksempel på en `api_klient` i test-miljø. Her er noen tips til utfylling:
     * Pass på å velge følgende scopes: `openid`, `altinn:instances.read` og `altinn:instances.write`
     * Den verdien du setter i "Navn på integrasjonen" vil vises i innloggingsvinduet for sluttbruker. Angi derfor et navn som godt beskriver hva API-klienten skal brukes til. Feks: "DittFagsystem - Innrapportering til Register over reelle rettighetshavere" 
     * Når sluttbruker har logget inn gjennom ID-porten, må sluttbruker sendes tilbake til en gyldig `redirect-uri`. Denne eksempel-klienten har konfigurert følgende gyldige `redirect uri`-er for å forenkle testing:
       * https://test.superbrasluttbrukersystem.no/reelle/innrapportering - For å kunne sende brukere tilbake til tjeneste i testmiljø
       * https://oauth.pstmn.io/v1/callback - For å teste innlogging og innsending gjennom Postman må man kunne sendes tilbake til Postman
       * http://localhost:8080/reelle/innrapportering - For at utviklere skal skal kunne teste lokalt må man kunne sendes tilbake til localhost

Når API-klienten er opprettet er forutsetningene på plass for at du kan sende inn skjema på vegne av en bruker. [Se detaljer om innsendingsprosessen her.](../hvordan-sende-inn)


## Jeg trenger hjelp
Hvis du har problemer med å registrere en `api_klient` via Selvbetjeningsløsningen skal henvendelser i utgangspunktet gå til Digdir.
Kontakt servicedesk@digdir.no oppgi client_id og miljø og forklar problemet.
