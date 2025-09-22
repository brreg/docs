---
title: Integrasjon direkte mot BR
description: Beskrivelser av API innen BRs elektroniske mottak av meldinger
weight: 100
---

## Innledning

Brønnøysundregistrenes elektroniske mottak har et REST-grensesnitt som kan benyttes av eksterne parter for innsending av meldinger.

## Sikkerhetsmekanismer

Siden dette er begrensede API så skal kallende parter autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_overordnet.html).

For å kunne få tilgang til våre begrensede APIer må man bruke et JWT-token fra Maskinporten med scopet `brreg:mottak`

Access-tokenet oppgis i headeren `Authorization`. Husk `Bearer` før tokenet.

| Header        | Verdi                       |
|---------------|-----------------------------|
| Authorization | Bearer <maskinporten-token> |

## Innsending av melding

- Melding sendes inn via et POST-request til upload-endepunktet
- Requestet skal inneholde selve meldingen i request body samt eventuelle vedlegg, strukturert som multipart form-data
- Meldingen (definert i henhold til XSD) må inneholde en id-attributt, en UUID generert av avsender. Denne fungerer som avsenders referanse til meldingen (kalt meldingsId eller avsenders referanseId)

## Etter Innsending
- Når meldingen er validert og lagret, geenereres en ny UUID, kalt mottakId.
- Det sendes deretter en notifikasjon til riktig fagsystem/register basert på tjeneste og tjenestehandling oppgitt i meldingen.

## Behandling i fagsystemet
- Meldingen behandles av fagsystemet
  - Ved full automatisering kan dette ta sekunder.
  - ved manuell behandling kan det ta dager, avhengig av type melding.
- Når behandlingen er ferdig og vedtak fattes, opprettes en svarmelding.
  - Denne har egen meldingsId
  - Her vil meldingsId og mottakId være like
- Det legges ut informasjon på endepunktet outbound/available om at svarmeldingen er klar til nedlasting. Konsumenten må selv gjøre periodiske kall mot dette endepunktet for å sjekke etter nye meldinger.

## Håndtering av svarmeldinger

1. Nedlasting: 
    - Når en svarmelding er tilgjengelig, hentes den fra outbound/download ved å oppgi mottakId.
    - Responsen er en ZIP-fil som inneholder hendvendelse.xml.
      - Filen følger samme XSD som innsendte meldinger.
      - XML-en inneholder en konvolutt med metadata og et element Data med returnmeldingen.
      - Et Rereranse-element med referanseType="Meldingsreferanse" som peker tilbake til den opprinnelige meldingsId (avsenders referanseId)
2. Matching:
    - Konsumenten må matche svarmeldingens referanseId med meldingen som ble sendt inn opprinnelig, for å koble svaret til riktig forretningsprosess.
3. Bekreftelse:
    - Når svarmeldingen er behandlet hos konsumenten, skal outbound/confirm kalles med mottakId som parameter.
    - Dette gjør at informasjon om svarmeldingen fjernes fra outbound/available.

## Eksempel: Innsendt melding
```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Melding xmlns="http://schema.brreg.no/postmottak/henvendelse" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" id="aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa" tjeneste="tjenestenavn" tjenestehandling="tjenestehandlingnavn" versjon="4.0" xsi:schemaLocation="http://schema.brreg.no/postmottak/henvendelse melding_4.0.xsd">
  <Mottaker id="111111111" idType="Organisasjonsnummer"/>
  <Avsender id="222222222" idType="Organisasjonsnummer"/>
  <Innhold>
    <Data format=.....
```

Eksempel: Innholdet i svarmelding (hendvendelse.xml)
```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Melding xmlns="http://schema.brreg.no/postmottak/henvendelse" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" id="bbbbbbbb-bbbb-bbbb-bbbb-bbbbbbbbbbbb" tjeneste="tjenestenavn" tjenestehandling="vedtak" versjon="4.0" xsi:schemaLocation="http://schema.brreg.no/postmottak/henvendelse melding_4.0.xsd">
  <Mottaker id="222222222" idType="Organisasjonsnummer"/>
  <Avsender id="111111111" idType="Organisasjonsnummer"/>
  <Referanse referanse="aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa" referanseType="MeldingsReferanse"/>
  <Innhold>
    <Data format=.....
```
