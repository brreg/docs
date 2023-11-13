---
title: Virksomheter
description: Beskrivelse av tjeneste for oppslag/søk i Register over reelle rettighetshavere
weight: 100
---

`Virksomheter` er et API for oppslag/søk i Register over reelle rettighetshavere.

* API'et tilbyr opplysninger om registrerte virksomheter og deres reelle rettighetshavere ved oppslag med ulike
  parametere, samt nedlasting av registerets totalbestand
* APIet er tilgangsstyrt, se siden [Hvordan få tilgang?](../../tilgang-til-apier)
* Opplysningene om reelle rettighetshavere inkluderer fullt fødsels- eller D-nummer fra Folkeregisteret.
  API'et skjermer ikke opplysninger om mindreårige og andre som er unntatt fra innsyn

### API-spesifikasjon

APIet er tilgjengelig for konsumering gjennom Swagger-UI og som en nedlastbar OpenAPI-spesifikasjon. Her finner du
mer utfyllende informasjon om hva APIet tilbyr.

| Miljø      | Swagger-UI                           | OpenAPI-spesifikasjon                                    |
|------------|--------------------------------------|----------------------------------------------------------|
| Test       | https://rrh.ppe.brreg.no/api/oppslag | https://rrh.ppe.brreg.no/api/oppslag/openapi/openapi.zip |
| Produksjon | https://rrh.brreg.no/api/oppslag     | https://rrh.brreg.no/api/oppslag/openapi/openapi.zip     |

### Ordliste

Definisjoner på begrep som er brukt i denne dokumentasjonen.

| Begrep                | Definisjon                                                                                                                                        |
|:----------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------|
| Reell rettighetshaver | En reell rettighetshaver er en fysisk person som gjennom sin eierandel eller stemmeandel, alene eller sammen med andre, kontrollerer virksomheten |
| Swagger-UI            | Tjeneste for visualisering og interagering med et API                                                                                             |

### Kodeliste
Ved kall til våre API'er vil enkelte felter i responsene være kodeverdier.  
En kodeliste som inneholder alle relevante koder med beskrivelser kan du [laste ned her](rrh_kodeliste_virksomheter.xlsx).

### Løsningsmodell

![Tilgangsstyrt API løsningsmodell](https://github.com/brreg/informasjonsmodeller/blob/main/registeroverreellerettighetshavere/loesningsmodeller/tilgangsstyrt_api.jpg?raw=true)

