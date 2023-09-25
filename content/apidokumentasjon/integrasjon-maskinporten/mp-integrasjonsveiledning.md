---
title: Integrasjon mot Maskinporten
description: Veiledning for integrasjon mot Maskinporten
weight: 100
---


## Innledning

Tilgang til APIet krever autentisering via [Maskinporten](https://docs.digdir.no/maskinporten_guide_apikonsument.html).

Kort fortalt så må API-konsument initielt opprette en Maskinport-integrasjon (oauth2-klient) og registrere scopet til APIet til denne. 
Når APIet skal brukes, må denne oauth2-klienten forespørre et token fra Maskinporten og inkludere dette tokenet i kall til APIet.

Det er også blitt opprettet en referanseapplikasjon for å gjøre det enklere å se hvordan man skal integrere. 
Koden for denne er lagt ut i brreg sitt repository på github: https://github.com/brreg/refapp-integrasjon

**_MERK:_** API-konsument må en ha et gyldig virksomhetssertifikat, enten for et syntetisk organisasjonsnummer (testmiljø), eller for et gyldig organisasjonsnummer (produksjonsmiljø).


## Opprette Maskinport-integrasjon (oauth2-klient)

API-konsument trenger en oauth2-klient (også omtalt som klient) for å hente Maskinport-token for aktuelt scope, som må inkluderes i kall til APIet. 
Se [overordnet arkitekturbeskrivelse](https://docs.digdir.no/docs/Maskinporten/maskinporten_overordnet).

Integrasjonen/klienten kan opprettes manuelt i [Samarbeidsportalen](https://minside-samarbeid.digdir.no/organization-home/services/service-admin) eller via Maskinporten sitt [selvbetjeningsAPI](https://docs.digdir.no/oidc_api_admin_maskinporten.html). 
Da selvbetjeningsAPIet også er beskyttet av Maskinport-token, må API-konsument ha en egen oauth2-klient, også omtalt som selvbetjeningsklient, for å bruke denne tjenesten. 
Ta kontakt med [Digdir sin servicedesk](mailto:servicedesk@digdir.no) for å få en selvbetjeningsklient.

Klienten skal registreres for aktuelt scope, f.eks. `brreg:losore/utlegg`. Se dokumentasjon av APIene for informasjon om hvilket scope som skal brukes.

Maskinporten vil svare med en `client_id`.

**_MERK:_** **For løsøreregisteret:** En klient for et syntetisk organisasjonsnummer (testmiljø) må opprettes via selvbetjeningsAPIet. 
Selvbetjeningsklienter for API-konsumenter av ITU/UTT-API er allerede opprettet med identifikator `oidc_<fiktivt organisasjonsnummer>_api`.


## Hente access token

**_MERK_** Dette steget forutsetter at en klient allerede er opprettet med tilgang til aktuelt scope.

#### Lag Keystore

En keystore av typen JKS som inneholder virksomhetssertifikatet må opprettes, se [Maskinporten](https://docs.digdir.no/oidc_sample_jwtgrant_postman.html) for nærmere informasjon.

Dette kan gjøres i UNIX-systemer (Mac/Linux) ved å kjøre kommandoen:

```
keytool -v -importkeystore -srckeystore <filnavn> -srcstoretype PKCS12 (om virksomhetssertifikatet er av type .p12) -destkeystore <ønsket-navn-på-keystore> -deststoretype JKS
```

Etter input vil du først lage et passord for keystore, dette trenger du videre. Deretter blir en spurt om passordet til virksomhetssertifikatet. Skriv inn ønsket og gitt passord og keystore vil bli opprettet.

#### Hent JWT

Opprett en [properties fil med felter som beskrevet her](https://docs.digdir.no/maskinporten_guide_apikonsument.html#5-be-om-token).

Autentisering via Maskinporten foregår ved hjelp av JWT tokens. Digdir har laget en egen [JWT-grant-generator](https://github.com/difi/jwt-grant-generator) som lastes ned og bygges i henhold til dokumentasjonen som finnes på lenken.
Alternativt kan man ta utgangspunkt i brreg sin [refapp-integrasjon](https://github.com/brreg/refapp-integrasjon).

Flere av feltene vil JWT-grant-generator skape automatisk om denne brukes. Ved bruk av JWT-grant-generator, opprett en properties fil med feltene beskrevet i seksjonen for å generere JWT, med følgende endringer:

```properties
issuer=<client_id>
scope=<scope for API>
```

Scope kan f.eks. være `brreg:losore/utlegg`. Se dokumentasjon av APIene for informasjon om hvilket scope som skal brukes.

Ved kjøring av JWT-grant-generatoren vil en få ut et access token som kan brukes mot våre APIer.
