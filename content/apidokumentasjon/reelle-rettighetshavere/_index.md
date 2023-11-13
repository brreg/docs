---
title: Register over reelle rettighetshavere
description: Beskrivelser av API innen domene Reelle rettighetshavere
weight: 120
---

## Våre tjenester ## 
Register over reelle rettighetshavere tilbyr tjenester / API'er for uthenting av opplysninger fra registeret.  
Noen tjenester vil ha krav til tilgangsstyring, og det vil skje gjennom bruk av maskinporten.  
Virksomheter som er berettiget tilgang kan få tilgang til tilgangsstyrte tjenester ved å sende en [bestilling]({{<ref "./komme-i-gang#hvordan-bestiller-jeg-tilgang-til-tjenester">}}) til Brønnøysundregistrene.  
En virksomhet som har fått tilgang til tjenester vil kunne delegere denne tilgangen videre til en systemleverandør om ønskelig.

## Informasjonsmodeller ##
Informasjonsmodeller beskriver på en formalisert måte informasjon og sammenhengene mellom informasjonselementene innenfor forretningsområdet for registeret.  
Mer informasjon om hvilke typer informasjonsmodeller vi legger ut finner du [her]({{<ref "/informasjonsmodeller/_index.md">}}).  
Forretningsprosessmodeller og strukturmodeller for registeret finner du [her]({{<ref "/informasjonsmodeller/reelle-rettighetshavere/_index.md">}}).  
Løsningsmodeller vil du finne under de enkelte API-beskrivelsene.

## Testdata ##
Testdata om personer og virksomheter i våre tjenester vil være syntetiske.
Kilden til syntetiske data om personer og virksomheter er [Tenor](https://www.skatteetaten.no/skjema/testdata/) som er en tjeneste for testdatasøk som tilbys av Skatteetaten.  
For våre tjenester vil vi i tilknytning til den aktuelle tjenesten liste opp syntetiske testdata som konsumenter kan benytte under testing.  
Du kan se et eksempel på testdata [her]({{<ref "./oppslagstjenester/virksomheter/testdata_for_tilgangsstyrt_api.md">}})

## Versjonering
Vi versjonerer våre tjenester slik at vi kan gjøre oppdateringer uten for store konsekvenser for konsumentene.  
Vi benytter path-versjonering, noe som blant annet gjør det lett å se hvilken versjon man går mot til en hver tid.

### Versjoneringsstrategi
Vi vil forsøke så langt det lar seg gjøre å ikke bryte bakoverkompatibiliteten med våre brukere.  
Likevel kan det være nødvendig i enkelte situasjoner, av for eksempel juridiske årsaker eller vedlikehold, å gjøre endringer som fører til et slikt brudd.  
Vi vil i dette tilfellet versjonere tjenesten slik at nyeste versjon vil være tilgjengelig sammen med forrige versjon.  
Dette betyr at hvis du for øyeblikket går mot "/v1/ressurs" må du innen rimelig tid gå over til en nyere versjon, feks "/v2/ressurs".  
Eldre versjon vil anses som utdatert/deprecated, og vil på sikt bli tatt bort.  
Ved behov for denne typen endringer vil vi forsøke å gi bruker god tid, og varsle om endringen i forkant.

### Når innføres det en ny versjon?
Vi vil innføre en ny versjon når vi introduserer en endring som påvirker bakoverkompatibiliteten. Mindre endringer og patcher vil ikke medføre versjonsendring.  
Eksempel på endring som medfører versjonering:
* Fjerne eller endre navn på et attributt i HTTP-responsen
* Fjerne eller endre navn på et REST-endepunkt

### Når fjernes en versjon?
Vi vil legge ut varsel/driftsmeldinger i god tid på https://www.brreg.no/om-oss/driftsmeldinger/. I tillegg kan du abonnere på en RSS-feed [her](https://www.brreg.no/produkter-og-tjenester/rss-feed/).

{{% children /%}}

