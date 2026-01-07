---
title: Virksomheter
description: Beskrivelse av tjeneste for oppslag/søk i Register over reelle rettighetshavere
weight: 100
---

- [API-spesifikasjon](#api-spesifikasjon)
- [Løsningsmodell](#løsningsmodell)
- [Tilgang til endepunkter](#tilgang-til-endepunkter)
- [Tilgang til informasjon som er begrenset](#tilgang-til-informasjon-som-er-begrenset)
- [Hvordan bruke totalbestanden med endringsloggen](#hvordan-bruke-totalbestanden-med-endringsloggen)
- [Endringer i APIet](#endringer-i-apiet)

`Virksomheter` er et API for oppslag/søk i Register over reelle rettighetshavere.

* APIet tilbyr
    * Opplysninger om registrerte virksomheter og deres reelle rettighetshavere
    * Nedlasting av totalbestand på json-format
    * Endringslogg: Dette brukes typisk for å fange opp at det har skjedd endringer på registreringer om reelle
      rettighetshavere i registeret
    * Kodelister: Kan brukes til visning i eventuelle brukergrensesnitt, dynamisk oppdatering av kodelister, validering
      og lignende. Endepunktet er åpent, og krever ikke maskinporten-autentisering
    * Se [vår Swagger-dokumentasjon](https://rrh.brreg.no/api/oppslag) for mer mer informasjon om de forskjellige
      endepunktene, samt eksempler på forespørsler og responser
* Alle endepunktene i APIet med unntak av Kodelister er tilgangsstyrt,
  se [Tilgang til endepunkter](#tilgang-til-endepunkter)

## API-spesifikasjon

APIet er tilgjengelig for konsumering gjennom Swagger-UI og som en nedlastbar OpenAPI-spesifikasjon. Her finner du
mer utfyllende informasjon om hva APIet tilbyr.

| Miljø      | Swagger-UI                           | OpenAPI-spesifikasjon                                    |
|------------|--------------------------------------|----------------------------------------------------------|
| Test       | https://rrh.ppe.brreg.no/api/oppslag | https://rrh.ppe.brreg.no/api/oppslag/openapi/openapi.zip |
| Produksjon | https://rrh.brreg.no/api/oppslag     | https://rrh.brreg.no/api/oppslag/openapi/openapi.zip     |

## Løsningsmodell

Se løsningsmodell under informasjonsmodeller
for [Virksomhet](../../../../../informasjonsmodeller/reelle-rettighetshavere/loesningsmodeller/rrh_loesningsmodell_virksomhet)

## Tilgang til endepunkter

Vi tilbyr ulike [maskinporten-scopes](../../maskinporten/hvordan-bruke-maskinporten) til forskjellige aktører. Tabellen
under beskriver hvilke endepunkter maskinporten-scopene har tilgang til. Alle endepunktene i APIet med unntak av
Kodelister er tilgangsstyrt, se tabellen under for å finne ut hva ditt
maskinporten-scope har tilgang til.

| Aktør                                                                                                | Maskinporten-scope                                                                                                | Kodelister | Oppslag på virksomhetens organisasjonsnummer | Oppslag på fødselsnummer eller D-nummer | Nedlasting av totalbestand | Endringslogg |
|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|------------|----------------------------------------------|-----------------------------------------|----------------------------|--------------|
| Offentlig myndighet i § 3-11 (1)                                                                     | **brreg:reelle/offentlig**                                                                                        | X          | X                                            | X                                       | X                          | X            |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav a, b, c, e, g, h til k, n og o | **brreg:reelle/rapporteringspliktig**                                                                             | X          | X                                            |                                         |                            | X            |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav d, f, l og m                   | **brreg:reelle/rapporteringspliktig.begrenset**                                                                   | X          | X                                            |                                         |                            | X            |
| Medier, sivilsamfunnsorganisasjoner og høyere utdanningsinstitusjoner i § 3-11 (2), (3) og (4) ledd. | **brreg:reelle/media**, **brreg:reelle/sivilsamfunnsorganisasjon**, **brreg:reelle/hoeyereutdanningsinstitusjon** | X          | X                                            |                                         |                            | X            |                          
| Alle andre                                                                                           | **Krever ikke maskinporten-scope**                                                                                | X          |                                              |                                         |                            |              |

## Tilgang til informasjon som er begrenset

Se tabellen under for å finne ut om ditt maskinporten-scope har tilgang til å se fødselsnummer og D-Nummer. Full
oversikt over alle tilgjengelige
felter og særregler kan ses i løsningsmodell
for [virksomhet](../../../../../informasjonsmodeller/reelle-rettighetshavere/loesningsmodeller/rrh_loesningsmodell_virksomhet.md).

| Aktør                                                                                                | Maskinporten-scope                                                                                                | Fødselsnummer og D-nummer |  
|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|---------------------------|
| Offentlig myndighet i § 3-11 (1)                                                                     | **brreg:reelle/offentlig**                                                                                        | X                         |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav a, b, c, e, g, h til k, n og o | **brreg:reelle/rapporteringspliktig**                                                                             | X                         |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav d, f, l og m                   | **brreg:reelle/rapporteringspliktig.begrenset**                                                                   | X                         
| Medier, sivilsamfunnsorganisasjoner og høyere utdanningsinstitusjoner i § 3-11 (2), (3) og (4) ledd. | **brreg:reelle/media**, **brreg:reelle/sivilsamfunnsorganisasjon**, **brreg:reelle/hoeyereutdanningsinstitusjon** |                           |

Se tabellen under for hvilke data ditt maskinporten-scope har tilgang til å se om uoverensstemmelser.

| Aktør                                                                                                | Maskinporten-scope                                                                                                | Innhold i uoverensstemmelse og uoverensstemmelsesdato | Historiske uoverensstemmelser | Opplysninger om innsender |
|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|-------------------------------|---------------------------|
| Offentlig myndighet i § 3-11 (1)                                                                     | **brreg:reelle/offentlig**                                                                                        | X                                                     | X                             | X                         |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav a, b, c, e, g, h til k, n og o | **brreg:reelle/rapporteringspliktig**                                                                             | X                                                     |                               |                           |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav d, f, l og m                   | **brreg:reelle/rapporteringspliktig.begrenset**                                                                   | X                                                     |                               |                           |
| Medier, sivilsamfunnsorganisasjoner og høyere utdanningsinstitusjoner i § 3-11 (2), (3) og (4) ledd. | **brreg:reelle/media**, **brreg:reelle/sivilsamfunnsorganisasjon**, **brreg:reelle/hoeyereutdanningsinstitusjon** | X                                                     |                               |                           |

## Hvordan bruke totalbestanden med endringsloggen

Noen maskinporten scopes har tilgang til å laste ned totalbestanden over Register over reelle rettighetshavere.
Følgende er en veiledning for hvordan totalbestanden kan brukes sammen med endringsloggen for å opprettholde en
oppdatert, lokal kopi av registeret.
For hvert punkt, referer gjerne til Swagger-UI dokumentasjonen for et overblikk over hvordan responsene til endepunktene
ser ut.

**For å bygge opp en lokal kopi av Register over reelle rettighetshavere, gjør du følgende:**

1. Hent ut totalbestanden fra `/virksomheter/totalbestand` og lagre den i din lokale database.

**For å holde din lokale kopi oppdatert med nye endringer, gjør du følgende:**

1. Kall endepunktet `/sekvensnummer` med et tidspunkt noen dager før du tok ut totalbestanden. Endepunktet vil returnere
   et sekvensnummer, som vil være utgangspunktet ditt for å fange opp endringer fra `/endringslogg` i neste steg.
2. Sett opp en maskinell jobb der du jevnlig kaller endepunktet `/endringslogg`.
1. Kall `/endringslogg` med sekvensnummeret du fikk i det forrige steget. Dette vil returnere en logg over alle
   endringene som har skjedd i registeret, etter sekvensnummeret du fikk. Hver av disse endringene inneholder et
   organisasjonsnummer som brukes i det neste steget.
2. Fra hver endring, hent ut organisasjonsnummeret og gjør et kall mot `/virksomhet/{organisasjonsnummer}`. Dette vil
   returnere organisasjonens registreringer. Da kan du sammenligne dine lokale registreringer for organisasjonen, med de
   i Register over reelle rettighetshavere. Oppdater din lokale kopi dersom registreringene dine er forskjellige.
3. Oppdater sekvensnummeret ditt til den siste endringens `id`. Da har du det nyeste sekvensnummeret, som kan brukes til
   å kalle `/endringslogg` igjen for å lytte på videre endringer.

Hvis det er lenge siden du har oppdatert kopien din, kan det lønne seg å heller hente ut totalbestanden på nytt så du
slipper å gå igjennom hele endringsloggen.
Totalbestanden oppdateres normalt ved midnatt hver dag, men dette er ikke garantert. For å være trygg på at du får med
deg alle endringer, anbefaler vi å bruke `/sekvensnummer` med et tidspunkt noen dager før uttaket av totalbestanden.

## Endringer i APIet

Her dokumenteres alle endringer som er gjort på Virksomhet APIet for Reelle Rettighetshavere.  
Formatet er basert på [keep a changelog](https://keepachangelog.com/en/1.1.0/)
og dette prosjektet følger [semantisk versjonering](https://semver.org/spec/v2.0.0.html).

### 1.5.4 - 2026-01-07

#### Endret
 
Korrigert følgende eksempler i OpenAPI-spesifikasjonen:

- Finn registreringspliktige virksomheter (`/v1/virksomheter`)
- Hent neste sekvensnummer (`/v1/sekvensnummer`)
- Hent registreringspliktig virksomhet (`/v1/virksomheter/{organisasjonsnummer}`)
- Totalbestand (`/v1/virksomheter/totalbestand`)


### 1.5.3 - 2025-12-15

#### Endret

Rettet feil i OpenAPI-spesifikasjon for endepunkt for å hente endringslogg: `/v1/endringslogg`:

- Enkelte felter på EndringsloggResponse-objektet som var feilaktig markert som optional er nå required. Dette gjelder følgende felt:
  - `specversion`
  - `id`
  - `source`
  - `type`
  - `time`
- **Merk:** API-atferden er uendret — kun dokumentasjonen er korrigert.


### 1.5.2 - 2025-12-09

#### Endret

Rettet feil i OpenAPI-spesifikasjon for endepunkt for å hente sekvensnummer etter dato: `/v1/sekvensnummer`:

- Felt `sekvensnummer` i SekvensnummerResponse-objektet er nå markert som required.
- **Merk:**  API-atferden er uendret — kun dokumentasjonen er korrigert.

Rettet feil i OpenAPI-spesifikasjon for endepunkt for enkeltsopplag på organisasjonsnummer:
`/v1/virksomheter/{organisasjonsnummer}`.

- Enkelte felter som var feilaktig markert som optional er nå required. Dette gjelder følgende felt:
    - `internettadresse` (RegulertMarked-objektet)
    - `adresse` (UtenlandskVirksomhet-objektet)
- Enkelte listefelter som var feilaktig markert som optional er nå required. Hvis listen ikke har noen elementer får man
  en tom liste. Dette gjelder feltene:
    - `mellomliggendeVirksomheter` (Posisjon-objektet)
    - `statsborgerskap` (Person-objektet)

- Enkelte felter på personrelaterte objekter som var feilaktig markert som required er nå optional. Dette gjelder
  følgende
  felt:
    - `foedselsEllerDNummer` (Person-objektet)
        - Se tabell over for å se hvilke Maskinporten-scopes som har tilgang til feltet.
    - `navn` (Person-objektet)
    - `foedselsdato` (UtenlandskPerson-objektet)
    - `fulltNavn` (UtenlandskPerson-objektet)
    - **Merk:** Bakgrunnen for endringen er at noen Maskinporten-scopes ikke har tilgang til disse feltene når personen
      i responsen er unntatt fra innsyn.
- **Merk:**  API-atferden er uendret — kun dokumentasjonen er korrigert.

### 1.5.1 - 2025-11-11

#### Endret

- Tar i bruk landkode "XUK" (Uoppgitt) når bostedsland for person er ukjent. Tidligere returnerte APIet verdien "
  UKJENT".

### 1.5.0 - 2025-06-30

### Lagt til

* Endringer på klassen Uoverensstemmelse
  i [løsningsmodellen](../../../../../informasjonsmodeller/reelle-rettighetshavere/loesningsmodeller/rrh_loesningsmodell_virksomhet/)
    * Nytt felt innsender på uoverensstemmelse. En innsender kan være:
        * En utenlandsk person
        * En folkeregistrert person
        * Eller en norsk virksomhet

### 1.4.0 - 2025-03-28

### Lagt til

* Gitt tilgang til endepunkt for å hente endringslogg til følgende Maskinporten-scope:
    * brreg:reelle/offentlig (Hadde tilgang fra før)
    * brreg:reelle/rapporteringspliktig
    * brreg:reelle/rapporteringspliktig.begrenset
    * brreg:reelle/media
    * brreg:reelle/sivilsamfunnsorganisasjon
    * brreg:reelle/hoeyereutdanningsinstitusjon

### 1.3.0 - 2025-03-21

#### Lagt til

* Vi tilgjengeliggjør nå en registrering med registreringsstatus `registreringsstatus.rettighetsinformasjonErIkkeMeldt`
  for alle registreringspliktige virksomheter i Register over reelle rettighetsavere.
    * Denne typen registrering er opprettet av Brønnøysundregistrene, og indikerer at virksomheten er
      registeringspliktig i registeret.
    * **Merk:** Hvis oppslag på opplysninger om reelle rettighetshavere returnerer `404 - NOT FOUND` indikerer det at
      virksomheten ikke er registreringspliktig og kan dermed ikke registrere seg i registeret.
* Ny type `no.brreg.rrh.rettighetsinformasjon.klargjortForRegistrering` i responsen til endringsloggen for
  registreringer med registreringsstatus `registreringsstatus.rettighetsinformasjonErIkkeMeldt`

### 1.2.1 - 2025-03-21

#### Lagt til

* Tabell over tilgang til data om `uoverensstemmelse`

### 1.2.0 - 2025-03-06

#### Lagt til

* Registreringer kan nå inneholde opplysninger om `uoverensstemmelse`
    * Se løsningsmodellen for mer informasjon.

### 1.1.0 - 2024-10-24

#### Lagt til

* Språkstøtte for kodelisteverdier
    * Det er introdusert et nytt parameter som muliggjør uthenting av responser med kodelisteverdier også på nynorsk og
      engelsk.
    * Funksjonaliteten er implementert på følgende endepunkter: `hentRegistreringspliktigVirksomhet`,
      `finnRegistreringspliktigeVirksomheter`, `hentRelevanteKodelister`
    * Funksjonaliteten er implementert i form av en frivillig HTTP-header: `Accept-Language`. Mulige verdier for
      headeren: `nob` (bokmål), `nno` (nynorsk) og `eng` (engelsk)
    * Hvis `Accept-Language`-headeren ikke er spesifisert eller er spesifisert med en ugyldig verdi, vil responsen
      returnere verdier på Bokmål som standard.

### 1.0.0 - 2024-09-28

API-ene er ikke lenger i beta-fasen og kan nå anses som stabile.

### 1.0.0-beta2 - 2024-02-28

#### Lagt til

- Nytt endepunkt for å hente en liste med alle tilgjenglige kodelister. Dette endepunktet kan feks. brukes til
  visning i eventuelle brukergrensesnitt, dynamisk oppdatering av kodelister, validering og lignende.

#### Endret

- Funksjonalitet for oppslag på virksomhet er endret til å inkludere opplysninger om både nåværende og tidligere
  registrerte reelle rettighetshavere.
- Søk på fødselsnummer er oppdatert til å gi en liste over virksomheter hvor personen, identifisert ved det angitte
  fødsels- eller D-nummeret, er eller har vært registrert som reell rettighetshaver.
