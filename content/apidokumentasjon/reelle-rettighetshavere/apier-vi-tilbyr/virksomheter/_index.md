---
title: Virksomheter
description: Beskrivelse av tjeneste for oppslag/søk i Register over reelle rettighetshavere
weight: 100
---

`Virksomheter` er et API for oppslag/søk i Register over reelle rettighetshavere.

* APIet tilbyr opplysninger om registrerte virksomheter og deres reelle rettighetshavere ved oppslag med ulike
  parametere, samt nedlasting av registerets totalbestand
* APIet er tilgangsstyrt, se siden [Tilgang til APIer](../../tilgang-til-apier)
* Opplysningene om reelle rettighetshavere inkluderer fullt fødsels- eller D-nummer fra Folkeregisteret.
  API'et skjermer ikke opplysninger om mindreårige og andre som er unntatt fra innsyn

## API-spesifikasjon

APIet er tilgjengelig for konsumering gjennom Swagger-UI og som en nedlastbar OpenAPI-spesifikasjon. Her finner du
mer utfyllende informasjon om hva APIet tilbyr.

| Miljø      | Swagger-UI                           | OpenAPI-spesifikasjon                                    |
|------------|--------------------------------------|----------------------------------------------------------|
| Test       | https://rrh.ppe.brreg.no/api/oppslag | https://rrh.ppe.brreg.no/api/oppslag/openapi/openapi.zip |

## Kodeliste
Ved kall til våre API'er vil enkelte felter i responsene være kodeverdier.  
En kodeliste som inneholder alle relevante koder med beskrivelser kan du [laste ned her](rrh_kodeliste_virksomheter.xlsx).

## Løsningsmodell

![Tilgangsstyrt API løsningsmodell](https://github.com/brreg/informasjonsmodeller/blob/main/registeroverreellerettighetshavere/loesningsmodeller/løsningsmodell_api_virksomheter.png?raw=true)

| **Klasse**                         | Egenskap                                           | Beskrivelse                                                                                                                                                    |
|------------------------------------|----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RegistreringspliktigVirksomhet** |                                                    | Virksomhet som er registreringspliktig i Register over reelle rettighetshavere                                                                                 |
|                                    | organisasjonsnummer                                | Organisasjonsnummer for registreringspliktig virksomhet                                                                                                        |
|                                    | navn                                               | Virksomhetsnavn for registreringspliktig virksomhet                                                                                                            |
|                                    | organisasjonsform                                  | Organisasjonsform for registreringspliktig virksomhet                                                                                                          |
|                                    | slettetIEnhetsregisteret                           | Dato for når registreringspliktig virksomhet ble slettet i Enhetsregisteret                                                                                    |
|                                    | førstRegistrertIRegisterOverReelleRettighetshavere | Dato for når registreringspliktig virksomhet første gang ble registrert i Register over reelle rettighetshavere                                                |
|                                    | slettetIRegisterOverReelleRettighetshavere         | Dato for når registreringspliktig virksomhet ble slettet i Register over reelle rettighetshavere                                                               |
| **Registrering**                   |                                                    | Melding om nyregistrering, endring eller sletting av opplysninger om reelle rettighetshavere                                                                   |
|                                    | registreringsid                                    | Unik identifikator for en bestemt registrering                                                                                                                 |
|                                    | registreringsstatus                                | Status på melding om registrering av reelle rettighetshavere                                                                                                   |
|                                    | registrert                                         | Dato for når registrering av reelle rettighetshavere ble godkjent                                                                                              |
|                                    | erGjeldendeRegistrering                            | Boolsk verdi som indikerer om gjeldende registrering er siste registrerte opplysninger om reelle rettighetshavere                                              |
|                                    | reelleRettighetshaverestatus                       | Angir om virksomheten har reelle rettighetshavere eller ikke                                                                                                   |
| **UtenlandskRegister**             |                                                    | Utenlandsk register over reelle rettighetshavere                                                                                                               |
|                                    | land                                               | Landkode for det utenlandske registeret                                                                                                                        |
|                                    | internettadresse                                   | Internettadresse for det utenlandske registeret                                                                                                                |
| **Marked**                         |                                                    | Marked for kjøp og salg av finansielle instrumenter, som er i samsvar med objektive handelsregler fastsatt av markedet selv og kravene i verdipapirhandelloven |
|                                    | navn                                               | Navn på det regulerte markedet                                                                                                                                 |
|                                    | land                                               | Landkode for det regulerte markedet                                                                                                                            |
|                                    | internettadresse                                   | Internettadresse for det regulerte markedet                                                                                                                    |
| **ReellRettighetshaver**           |                                                    | Fysisk person som i siste instans eier eller kontrollerer en registreringspliktig virksomhet                                                                   |
|                                    | erUnntattFraInnsyn                                 | Boolsk verdi som indikerer om reell rettighetshaver er mindreårig og dermed unntatt fra innsyn                                                                 |
|                                    | førstRegistrert                                    | Dato for når reell rettighetshaver ble registrert i Register over reelle rettighetshavere første gaang                                                         |
|                                    | endret                                             | Dato for når reell rettighetshaver sist ble endret i Register over reelle rettighetshavere                                                                     |
|                                    | slettet                                            | Dato for når reell rettighetshaver ble slettet i Register over reelle rettighetshavere                                                                         |
| **Posisjon**                       |                                                    | Type kontroll eller eierskap den reelle rettighetshaveren utøver overfor den registreringspliktige virksomheten i siste instans                                |
|                                    | posisjonstype                                      | En type kontroll eller eierskap over registreringspliktig virksomhet i siste instans                                                                           |
|                                    | størrelsesintervall                                | Hvor stor prosentandel reell rettighetshaver har av posisjon eierskap eller posisjon stemmerettigheter                                                         |
|                                    | beskrivelseAvPosisjonenKontrollPåAnnenMåte         | Tekstlig beskrivelse av posisjonen "kontroll på annen måte"                                                                                                    |
|                                    | grunnlagstype                                      | Grunnlag for posisjonen til den reelle rettighetshaveren                                                                                                       |
| **Person**                         |                                                    | Folkeregistrert person                                                                                                                                         |
|                                    | fødselsEllerDNummer                                | Fødselsnummer eller d-nummer for folkeregistrert person                                                                                                        |
|                                    | fødselsdato                                        | Fødselsdato for folkeregistrert person                                                                                                                         |
|                                    | fødselsår                                          | Fødselsår for folkeregistrert person                                                                                                                           |
|                                    | navn                                               | Fullt navn for folkeregistrert person                                                                                                                          |
|                                    | erDød                                              | Boolsk verdi som indikerer om folkeregistrert person er død                                                                                                    |
|                                    | bostedsland                                        | Bostedsland for folkeregistrert person                                                                                                                         |
|                                    | statsborgerskap                                    | Statsborgerskap for folkeregistrert person                                                                                                                     |
| **UtenlandskPerson**               |                                                    | Utenlandsk person uten fødselsnummer eller d-nummer                                                                                                            |
|                                    | fødselsdato                                        | Fødselsdato for utenlandsk person                                                                                                                              |
|                                    | fødselsår                                          | Fødselsår for utenlandsk person                                                                                                                                |
|                                    | fulltNavn                                          | Fullt navn for utenlandsk person                                                                                                                               |
|                                    | bostedsland                                        | Bostedsland for utenlandsk person                                                                                                                              |
|                                    | statsborgerskap                                    | Statsborgerskap for utenlandsk person                                                                                                                          |
| **MellomliggendeVirksomhet**       |                                                    | En eller flere juridiske personer som danner "lenken" mellom registreringspliktig virksomhet og reell rettighetshaver                                          |
| **NorskVirksomhet**                |                                                    | Norsk mellomliggende virksomhet                                                                                                                                |
|                                    | organisasjonsnummer                                | Organisasjonsnummer for den norske mellomliggende virksomheten                                                                                                 |
|                                    | navn                                               | Virksomhetsnavn for den norske mellomliggende virksomheten                                                                                                     |
|                                    | organisasjonsform                                  | Organisasjonsform for den norske mellomliggende virksomheten                                                                                                   |
|                                    | slettetIEnhetsregisteret                           | Dato for når den mellomliggende virksomheten ble slettet i Enhetsregisteret                                                                                    |
| **UtenlandskVirksomhet**           |                                                    | Utenlandsk mellomliggende virksomhet                                                                                                                           |
|                                    | registreringsnummerIHjemlandet                     | Registreringsnummer i hjemlandet for den utenlandske mellomliggende virksomheten                                                                               |
|                                    | navn                                               | Virksomhetsnavn for den utenlandske mellomliggende virksomheten                                                                                                |
| **InternasjonalAdresse**           |                                                    | Adresse for utenlandsk mellomliggende virksomhet                                                                                                               |
|                                    | friAdressetekst                                    | Adresse for den utenlandske mellomliggende virksomheten. Kan bestå av flere adresselinjer                                                                      |
|                                    | land                                               | Landkode og navn på hjemlandet til den utenlandske mellomliggende virksomheten                                                                                 |
