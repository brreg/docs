---
title: Hvem kan få tilgang til hva?
description: Informasjon om hva man får tilgang til fra våre APIer
weight: 2
---

Vi tilbyr ulike [maskinporten-scopes](../../maskinporten/hvordan-bruke-maskinporten) til forskjellige aktører, denne
siden beskriver hvilke endepunkt og informasjon de forskjellige maskinporten-scopene har tilgang til.

## API-tilgang for de ulike aktørene

* APIets endepunkt gir tilgang til:
  * Opplysninger om registrerte virksomheter og deres reelle rettighetshavere
  * Nedlasting av totalbestand på json-format
  * Endringslogg: dette brukes typisk for å fange opp at det har skjedd endringer på registreringer om reelle rettighetshavere i registeret
  * Kodelister: kan brukes til visning i eventuelle brukergrensesnitt, dynamisk oppdatering av kodelister, validering
   og lignende. endepunktet er åpent, og krever ikke maskinporten-autentisering

Alle endepunktene i APIet med unntak av Kodelister er tilgangsstyrt, se tabellen under for å finne ut hva ditt
Maskinporten-scope har
tilgang til.

| Aktør                                                                                                | Maskinporten-scope                                                                                                | Kodelister | Oppslag på virksomhetens organisasjonsnummer | Oppslag på fødselsnummer eller D-nummer | Nedlasting totalbestand | Endringslogg |
|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|------------|----------------------------------------------|-----------------------------------------|-------------------------|--------------|
| Offentlig myndighet i § 3-11 (1)                                                                     | **brreg:reelle/offentlig**                                                                                        | X          | X                                            | X                                       | X                       | X            |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav a, b, c, e, g, h til k, n og o | **brreg:reelle/rapporteringspliktig**                                                                             | X          | X                                            |                                         |                         |              |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav d, f, l og m                   | **brreg:reelle/rapporteringspliktig.begrenset**                                                                   | X          | X                                            |                                         |                         |              |
| Medier, sivilsamfunnsorganisasjoner og høyere utdanningsinstitusjoner i § 3-11 (2), (3) og (4) ledd. | **brreg:reelle/media**, **brreg:reelle/sivilsamfunnsorganisasjon**, **brreg:reelle/hoeyereutdanningsinstitusjon** | X          | X                                            |                                         |                         |              |                          
| Alle andre                                                                                           | **Krever ikke Maskinporten-scope**                                                                                | X          |                                              |                                         |                         |              |

## Informasjon som er begrenset

Se tabellen under for å finne ut om ditt Maskinporten-scope har tilgang til å se fødselsnummer og D-Nummer. Full oversikt over alle tilgjengelige
felter og særregler kan ses i løsningsmodell
for [virksomhet](../../../../../informasjonsmodeller/reelle-rettighetshavere/loesningsmodeller/virksomhet/rrh_loesningsmodell_virksomhet).

| Aktør                                                                                                | Maskinporten-scope                                                                                                | Fødselsnummer og D-nummer |  
|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|---------------------------|
| Offentlig myndighet i § 3-11 (1)                                                                     | **brreg:reelle/offentlig**                                                                                        | X                         |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav a, b, c, e, g, h til k, n og o | **brreg:reelle/rapporteringspliktig**                                                                             | X                         |
| Rapporteringspliktige etter hvitvaskingsloven § 4 første ledd bokstav d, f, l og m                   | **brreg:reelle/rapporteringspliktig.begrenset**                                                                   | X                         
| Medier, sivilsamfunnsorganisasjoner og høyere utdanningsinstitusjoner i § 3-11 (2), (3) og (4) ledd. | **brreg:reelle/media**, **brreg:reelle/sivilsamfunnsorganisasjon**, **brreg:reelle/hoeyereutdanningsinstitusjon** |                           |

