---
title: Eksempler
description: Eksempler på hvordan en registrering kan se ut
weight: 3
---

{{< warning >}}
Eksemplene beskriver det vi anser som 5 ganske vanlige innrapporteringer. Eksemplene er bygd opp med en tekstlig 
beskrivelse, en tabell som viser felter sluttbrukersystem må sette, og et eksempel på en maskinell innrapportering i 
JSON-format.
{{< /warning >}}

<!-- TOC -->

* [Eksempel 1: Eneaksjonær i et AS](#eksempel-1-eneaksjonær-i-et-as)
* [Eksempel 2: To reelle rettighetshavere i et AS, en norsk og en utenlandsk](#eksempel-2-to-reelle-rettighetshavere-i-et-as-en-norsk-og-en-utenlandsk)
* [Eksempel 3: En reell rettighetshaver med en mellomliggende virksomhet](#eksempel-3-en-reell-rettighetshaver-med-en-mellomliggende-virksomhet)
* [Eksempel 4: Fire reelle rettighetshavere med hver sin posisjon](#eksempel-4-fire-reelle-rettighetshavere-med-hver-sin-posisjon)
* [Eksempel 5: Fem reelle rettighetshavere som eier 20% hver](#eksempel-5-fem-reelle-rettighetshavere-som-eier-20-hver)

<!-- TOC -->

## Eksempel 1: Eneaksjonær i et AS

Snekkeren AS har fått melding i Altinn fra Register over reelle rettighetshavere om at virksomheten må registrere sine
reelle rettighetshavere. Virksomheten benytter et sluttbrukersystem som tilbyr en løsning for maskinell
innrapportering. Ole Olsen er eneaksjonær i Snekkeren AS. En av de som har tilgang logger seg inn på sitt 
sluttbrukersystem, sørger for å rapportere for Snekkeren AS, og sender inn opplysninger om reelle 
rettighetshavere.

| Opplysninger som skal sendes inn                                                 | JSON-sti                                                                                                                | JSON-verdi                                                     |
|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Virksomhetens organisasjonsnummer                                                | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                                             | 310956643                                                      |
| Har virksomheten reelle rettighetshavere                                         | skjemainnhold.skjemadata.reelleRettighetshavereidentifikasjon                                                           | reellerettighetshavereidentifikasjon.harReelleRettighetshavere |
| Finnes det noen rettighetshavere som ikke kan identifiseres                      | skjemainnhold.skjemadata.kanIkkeIdentifisereFlereReelleRettighetshavere                                                 | false                                                          |
| *Ole Olsen*                                                                      |                                                                                                                         |                                                                |
| Er personen registrert i folkeregisteret                                         | skjemainnhold.skjemadata.reellRettighetshaver[0].erRegistrertIFolkeregisteret                                           | true                                                           |
| Fødselsnummer                                                                    | skjemainnhold.skjemadata.reellRettighetshaver[0].folkeregistrertPerson.foedselsEllerDNummer                             | 41864000647                                                    |
| Har posisjon eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonEierskap                                                    | true                                                           |
| Har posisjon kontroll over stemmerettigheter                                     | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonKontrollOverStemmerettigheter                               | false                                                          |
| Har posisjon kontroll på annen måte                                              | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonKontrollPaaAnnenMaate                                       | false                                                          |
| Har posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene | false                                                          |
| Har posisjon avgitt grunnkapital                                                 | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonAvgittGrunnkapital                                          | false                                                          |
| Har posisjon rett til å utpeke et flertall av styremedlemmene                    | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene                  | false                                                          |
| Har posisjon destinatar                                                          | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonDestinatar                                                  | false                                                          |
| Har posisjon særlige rettigheter                                                 | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonSaerligeRettigheter                                         | false                                                          |
| Eierskap størrelsesintervall 75% - 100%                                          | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.stoerrelsesintervall                                  | stoerrelsesintervall.intervall3                                |
| Grunnlag for eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.grunnlag                                              | grunnlagstype.direkte                                          |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
  "versjon": "1.0.0",
  "endret": "2024-08-12",
  "skjemainnhold": {
    "metadata": {
      "tjeneste": "rrh.ktr.reelle",
      "tjenestehandling": "nyregistrering",
      "rettighetsinformasjonsid": "RRH202400000196",
      "registreringsid": "c3f70fff-b72b-4439-887c-11b30087816b"
    },
    "fagsystem": {
      "organisasjonsnummer": null,
      "navn": null
    },
    "integrasjon": {
      "hfHentPreutfyllingFeilet": false,
      "hfHentRollerFeilet": null
    },
    "skjemadata": {
      "registreringspliktigVirksomhet": {
        "organisasjonsnummer": "312807629",
        "hfSoekOrganisasjonsnummerFeilkode": null,
        "hfNavn": "Snekkeren AS",
        "hfOrganisasjonsform": "AS",
        "hfForretningsadresse": null,
        "hfNavnPaaHovedvirksomhetRegistrertIEoes": null,
        "hfLandnavnForHovedvirksomhetRegistrertIEoes": null,
        "hfSoekPaaOrganisasjonsnummer": null
      },
      "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
      "aarsakTilAtVirksomhetIkkeHarReelleRettighetshavere": null,
      "finnesDetReelleRettighetshavereITilleggTilRolleinnehavereForStiftelse": null,
      "reellRettighetshaver": [
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "41864000647"
          },
          "harPosisjonEierskap": true,
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonKontrollPaaAnnenMaate": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false,
          "posisjonEierskap": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall3",
            "grunnlag": "grunnlagstype.direkte"
          }
        }
      ],
      "kanIkkeIdentifisereFlereReelleRettighetshavere": false,
      "erVirksomhetRegistrertPaaRegulertMarked": null,
      "regulertMarked": null,
      "erReelleRettighetshavereRegistrertIUtenlandskRegister": null,
      "utenlandskRegister": null,
      "rolleinnehaver": null
    }
  }
}
{{< /expandableCode >}}

## Eksempel 2: To reelle rettighetshavere i et AS, en norsk og en utenlandsk

Snekkeren AS har fått melding i Altinn fra Register over reelle rettighetshavere om at virksomheten må registrere sine
reelle rettighetshavere. Virksomheten benytter et sluttbrukersystem som tilbyr en løsning for maskinell
innrapportering. Ole Olsen og Svante Turesson (er svensk, men har både svensk og amerikansk statsborgerskap) eier 50%
hver i Snekkeren AS. En av de som har tilgang logger seg inn på sitt sluttbrukersystem, sørger for å rapportere for 
Snekkeren AS, og sender inn opplysninger om reelle rettighetshavere.

| Opplysninger som skal sendes inn                                                 | JSON-sti                                                                                                                | JSON-verdi                                                     |
|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Virksomhetens organisasjonsnummer                                                | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                                             | 310561649                                                      |
| Har virksomheten reelle rettighetshavere                                         | skjemainnhold.skjemadata.reelleRettighetshavereidentifikasjon                                                           | reellerettighetshavereidentifikasjon.harReelleRettighetshavere |
| Finnes det noen rettighetshavere som ikke kan identifiseres                      | skjemainnhold.skjemadata.kanIkkeIdentifisereFlereReelleRettighetshavere                                                 | false                                                          |
| *Ole Olsen*                                                                      |                                                                                                                         |                                                                |
| Er personen registrert i folkeregisteret                                         | skjemainnhold.skjemadata.reellRettighetshaver[0].erRegistrertIFolkeregisteret                                           | true                                                           |
| Fødselsnummer                                                                    | skjemainnhold.skjemadata.reellRettighetshaver[0].folkeregistrertPerson.foedselsEllerDNummer                             | 41864000647                                                    |
| Har posisjon eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonEierskap                                                    | true                                                           |
| Har posisjon kontroll over stemmerettigheter                                     | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonKontrollOverStemmerettigheter                               | false                                                          |
| Har posisjon kontroll på annen måte                                              | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonKontrollPaaAnnenMaate                                       | false                                                          |
| Har posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene | false                                                          |
| Har posisjon avgitt grunnkapital                                                 | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonAvgittGrunnkapital                                          | false                                                          |
| Har posisjon rett til å utpeke et flertall av styremedlemmene                    | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene                  | false                                                          |
| Har posisjon destinatar                                                          | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonDestinatar                                                  | false                                                          |
| Har posisjon særlige rettigheter                                                 | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonSaerligeRettigheter                                         | false                                                          |
| Eierskap størrelsesintervall  50% - 74,99%                                       | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.stoerrelsesintervall                                  | stoerrelsesintervall.intervall2                                |
| Grunnlag for eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.grunnlag                                              | grunnlagstype.direkte                                          |
| *Svante Turesson*                                                                |                                                                                                                         |                                                                |
| Er personen registrert i folkeregisteret                                         | skjemainnhold.skjemadata.reellRettighetshaver[1].erRegistrertIFolkeregisteret                                           | false                                                          |
| Fødselsdato for                                                                  | skjemainnhold.skjemadata.reellRettighetshaver[1].utenlandskPerson.foedselsdato                                          | 1982-01-01                                                     |
| Fullt navn                                                                       | skjemainnhold.skjemadata.reellRettighetshaver[1].utenlandskPerson.fulltNavn                                             | Svante Turesson                                                |
| Bostedsland: Sverige                                                             | skjemainnhold.skjemadata.reellRettighetshaver[1].utenlandskPerson.bostedsland                                           | SWE                                                            |
| Statsborgerskap: Sverige og USA                                                  | skjemainnhold.skjemadata.reellRettighetshaver[1].utenlandskPerson.statsborgerskap                                       | SWE,USA                                                        |
| Har posisjon eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonEierskap                                                    | true                                                           |
| Har posisjon kontroll over stemmerettigheter                                     | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonKontrollOverStemmerettigheter                               | false                                                          |
| Har posisjon kontroll på annen måte                                              | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonKontrollPaaAnnenMaate                                       | false                                                          |
| Har posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene | false                                                          |
| Har posisjon avgitt grunnkapital                                                 | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonAvgittGrunnkapital                                          | false                                                          |
| Har posisjon rett til å utpeke et flertall av styremedlemmene                    | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene                  | false                                                          |
| Har posisjon destinatar                                                          | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonDestinatar                                                  | false                                                          |
| Har posisjon særlige rettigheter                                                 | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonSaerligeRettigheter                                         | false                                                          |
| Eierskap størrelsesintervall  50% - 74,99%                                       | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.stoerrelsesintervall                                  | stoerrelsesintervall.intervall2                                |
| Grunnlag for eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.grunnlag                                              | grunnlagstype.direkte                                          |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
  "versjon": "1.0.0",
  "endret": "2024-08-12",
  "skjemainnhold": {
    "metadata": {
      "tjeneste": "rrh.ktr.reelle",
      "tjenestehandling": "nyregistrering",
      "rettighetsinformasjonsid": "RRH202400000195",
      "registreringsid": "a0d7d295-4156-47ab-b4d0-56151fe0e57c"
    },
    "fagsystem": {
      "organisasjonsnummer": null,
      "navn": null
    },
    "integrasjon": {
      "hfHentPreutfyllingFeilet": false,
      "hfHentRollerFeilet": null
    },
    "skjemadata": {
      "registreringspliktigVirksomhet": {
        "organisasjonsnummer": "310561649",
        "hfSoekOrganisasjonsnummerFeilkode": null,
        "hfNavn": "Snekkeren AS",
        "hfOrganisasjonsform": "AS",
        "hfForretningsadresse": null,
        "hfNavnPaaHovedvirksomhetRegistrertIEoes": null,
        "hfLandnavnForHovedvirksomhetRegistrertIEoes": null,
        "hfSoekPaaOrganisasjonsnummer": null
      },
      "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
      "aarsakTilAtVirksomhetIkkeHarReelleRettighetshavere": null,
      "finnesDetReelleRettighetshavereITilleggTilRolleinnehavereForStiftelse": null,
      "reellRettighetshaver": [
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "41864000647"
          },
          "harPosisjonEierskap": true,
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonKontrollPaaAnnenMaate": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false,
          "posisjonEierskap": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall2",
            "grunnlag": "grunnlagstype.direkte"
          }
        },
        {
          "erRegistrertIFolkeregisteret": false,
          "utenlandskPerson": {
            "foedselsdato": "1982-01-01",
            "fulltNavn": "Svante Turesson",
            "bostedsland": "SWE",
            "statsborgerskap": "SWE,USA"
          },
          "harPosisjonEierskap": true,
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonKontrollPaaAnnenMaate": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false,
          "posisjonEierskap": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall2",
            "grunnlag": "grunnlagstype.direkte"
          }
        }
      ],
      "kanIkkeIdentifisereFlereReelleRettighetshavere": false,
      "erVirksomhetRegistrertPaaRegulertMarked": null,
      "regulertMarked": null,
      "erReelleRettighetshavereRegistrertIUtenlandskRegister": null,
      "utenlandskRegister": null,
      "rolleinnehaver": null
    }
  }
}
{{< /expandableCode >}}

## Eksempel 3: En reell rettighetshaver med en mellomliggende virksomhet

Snekkeren AS har fått melding i Altinn fra Register over reelle rettighetshavere om at virksomheten må registrere sine
reelle rettighetshavere. Virksomheten benytter et sluttbrukersystem som tilbyr en løsning for maskinell
innrapportering. Ole Olsen er indirekte eier i Snekkeren AS fordi han eier 100% av aksjene i Trelast AS, som igjen eier
60% av aksjene i Snekkeren AS. Resterende 40 % av aksjene i Snekkeren AS er eid av ansatte som har under 25 % hver.
En av de som har tilgang logger seg inn på sitt sluttbrukersystem, sørger for å rapportere for Snekkeren AS, og sender 
inn opplysninger om reelle rettighetshavere.


| Opplysninger som skal sendes inn                                                 | JSON-sti                                                                                                                          | JSON-verdi                                                     |
|----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Virksomhetens organisasjonsnummer                                                | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                                                       | 310496081                                                      |
| Har virksomheten reelle rettighetshavere                                         | skjemainnhold.skjemadata.reelleRettighetshavereidentifikasjon                                                                     | reellerettighetshavereidentifikasjon.harReelleRettighetshavere |
| Finnes det noen rettighetshavere som ikke kan identifiseres                      | skjemainnhold.skjemadata.kanIkkeIdentifisereFlereReelleRettighetshavere                                                           | false                                                          |
| *Ole Olsen*                                                                      |                                                                                                                                   |                                                                |
| Er personen registrert i folkeregisteret                                         | skjemainnhold.skjemadata.reellRettighetshaver[0].erRegistrertIFolkeregisteret                                                     | true                                                           |
| Fødselsnummer                                                                    | skjemainnhold.skjemadata.reellRettighetshaver[0].folkeregistrertPerson.foedselsEllerDNummer                                       | 41864000647                                                    |
| Har posisjon eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonEierskap                                                              | true                                                           |
| Har posisjon kontroll over stemmerettigheter                                     | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonKontrollOverStemmerettigheter                                         | false                                                          |
| Har posisjon kontroll på annen måte                                              | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonKontrollPaaAnnenMaate                                                 | false                                                          |
| Har posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene           | false                                                          |
| Har posisjon avgitt grunnkapital                                                 | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonAvgittGrunnkapital                                                    | false                                                          |
| Har posisjon rett til å utpeke et flertall av styremedlemmene                    | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene                            | false                                                          |
| Har posisjon destinatar                                                          | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonDestinatar                                                            | false                                                          |
| Har posisjon særlige rettigheter                                                 | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonSaerligeRettigheter                                                   | false                                                          |
| Eierskap størrelsesintervall  50% - 74,99%                                       | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.stoerrelsesintervall                                            | stoerrelsesintervall.intervall2                                |
| Grunnlag for eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.grunnlag                                                        | grunnlagstype.indirekte                                        |
| Mellomliggende virksomhet                                                        | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.mellomliggendeVirksomhet[0].erUtenlandskVirksomhet              | false                                                          |
| Organisasjonsnummer til Trelast AS                                               | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.mellomliggendeVirksomhet[0].norskVirksomhet.organisasjonsnummer | 310219622                                                      |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
  "versjon": "1.0.0",
  "endret": "2024-08-12",
  "skjemainnhold": {
    "metadata": {
      "tjeneste": "rrh.ktr.reelle",
      "tjenestehandling": "nyregistrering",
      "rettighetsinformasjonsid": "RRH202400000194",
      "registreringsid": "d87c44bf-c257-4d41-9d5d-eda9a90b5cdb"
    },
    "fagsystem": {
      "organisasjonsnummer": null,
      "navn": null
    },
    "integrasjon": {
      "hfHentPreutfyllingFeilet": false,
      "hfHentRollerFeilet": null
    },
    "skjemadata": {
      "registreringspliktigVirksomhet": {
        "organisasjonsnummer": "310496081",
        "hfSoekOrganisasjonsnummerFeilkode": null,
        "hfNavn": "Snekkeren AS",
        "hfOrganisasjonsform": "AS",
        "hfForretningsadresse": null,
        "hfNavnPaaHovedvirksomhetRegistrertIEoes": null,
        "hfLandnavnForHovedvirksomhetRegistrertIEoes": null,
        "hfSoekPaaOrganisasjonsnummer": null
      },
      "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
      "aarsakTilAtVirksomhetIkkeHarReelleRettighetshavere": null,
      "finnesDetReelleRettighetshavereITilleggTilRolleinnehavereForStiftelse": null,
      "reellRettighetshaver": [
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "41864000647"
          },
          "harPosisjonEierskap": true,
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonKontrollPaaAnnenMaate": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false,
          "posisjonEierskap": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall2",
            "grunnlag": "grunnlagstype.indirekte",
            "mellomliggendeVirksomhet": [
              {
                "erUtenlandskVirksomhet": false,
                "norskVirksomhet": {
                  "organisasjonsnummer": "310219622"
                }
              }
            ]
          }
        }
      ],
      "kanIkkeIdentifisereFlereReelleRettighetshavere": false,
      "erVirksomhetRegistrertPaaRegulertMarked": null,
      "regulertMarked": null,
      "erReelleRettighetshavereRegistrertIUtenlandskRegister": null,
      "utenlandskRegister": null,
      "rolleinnehaver": null
    }
  }
}
{{< /expandableCode >}}

## Eksempel 4: Fire reelle rettighetshavere med hver sin posisjon

Snekkeren AS har fått melding i Altinn fra Register over reelle rettighetshavere om at virksomheten må registrere sine
reelle rettighetshavere. Virksomheten benytter et sluttbrukersystem som tilbyr en løsning for maskinell
innrapportering. Snekkeren AS har fire reelle rettighetshavere som har hver sin posisjon. Ole Olsen eier 26% av
aksjene. Hans Hansen eier 50% i Woods AS, som igjen eier 50% av Snekkeren AS, Han har en intern avtale om 28% 
stemmerettigheter i Snekkeren AS. Hilde Knutsen eier 10% av virksomheten, men har en intern avtale som gjør at hun har 
rett til å utpeke eller avsette mer enn halvparten av styremedlemmer. Bente Hansen er verge for en mindreårig aksjeeier 
som eier 40% av aksjene. En av de som har tilgang logger seg inn på sitt sluttbrukersystem, sørger for å rapportere for 
Snekkeren AS, og sender inn opplysninger om reelle rettighetshavere.

| Opplysninger som skal sendes inn                                                 | JSON-sti                                                                                                                                               | JSON-verdi                                                     |
|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Virksomhetens organisasjonsnummer                                                | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                                                                            | 313164926                                                      |
| Har virksomheten reelle rettighetshavere                                         | skjemainnhold.skjemadata.reelleRettighetshavereidentifikasjon                                                                                          | reellerettighetshavereidentifikasjon.harReelleRettighetshavere |
| Finnes det noen rettighetshavere som ikke kan identifiseres                      | skjemainnhold.skjemadata.kanIkkeIdentifisereFlereReelleRettighetshavere                                                                                | false                                                          |
| *Ole Olsen*                                                                      |                                                                                                                                                        |                                                                |
| Er personen registrert i folkeregisteret                                         | skjemainnhold.skjemadata.reellRettighetshaver[0].erRegistrertIFolkeregisteret                                                                          | true                                                           |
| Fødselsnummer for Ole Olsen                                                      | skjemainnhold.skjemadata.reellRettighetshaver[0].folkeregistrertPerson.foedselsEllerDNummer                                                            | 41864000647                                                    |
| Har posisjon eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonEierskap                                                                                   | true                                                           |
| Har posisjon kontroll over stemmerettigheter                                     | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonKontrollOverStemmerettigheter                                                              | false                                                          |
| Har posisjon kontroll på annen måte                                              | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonKontrollPaaAnnenMaate                                                                      | false                                                          |
| Har posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene                                | false                                                          |
| Har posisjon avgitt grunnkapital                                                 | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonAvgittGrunnkapital                                                                         | false                                                          |
| Har posisjon rett til å utpeke et flertall av styremedlemmene                    | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene                                                 | false                                                          |
| Har posisjon destinatar                                                          | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonDestinatar                                                                                 | false                                                          |
| Har posisjon særlige rettigheter                                                 | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonSaerligeRettigheter                                                                        | false                                                          |
| Eierskap størrelsesintervall 25,01% - 49,99%                                     | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.stoerrelsesintervall                                                                 | stoerrelsesintervall.intervall1                                |
| Grunnlag for eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.grunnlag                                                                             | grunnlagstype.direkte                                          |
| *Hans Hansen*                                                                    |                                                                                                                                                        |                                                                |
| Er personen registrert i folkeregisteret                                         | skjemainnhold.skjemadata.reellRettighetshaver[1].erRegistrertIFolkeregisteret                                                                          | true                                                           |
| Fødselsnummer                                                                    | skjemainnhold.skjemadata.reellRettighetshaver[1].folkeregistrertPerson.foedselsEllerDNummer                                                            | 27899995479                                                    |
| Har posisjon eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonEierskap                                                                                   | false                                                          |
| Har posisjon kontroll over stemmerettigheter                                     | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonKontrollOverStemmerettigheter                                                              | true                                                           |
| Har posisjon kontroll på annen måte                                              | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonKontrollPaaAnnenMaate                                                                      | false                                                          |
| Har posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene                                | false                                                          |
| Har posisjon avgitt grunnkapital                                                 | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonAvgittGrunnkapital                                                                         | false                                                          |
| Har posisjon rett til å utpeke et flertall av styremedlemmene                    | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene                                                 | false                                                          |
| Har posisjon destinatar                                                          | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonDestinatar                                                                                 | false                                                          |
| Har posisjon særlige rettigheter                                                 | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonSaerligeRettigheter                                                                        | false                                                          |
| Stemmerettighet størrelsesintervall 25,01% - 49,99%                              | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.stoerrelsesintervall                                                                 | stoerrelsesintervall.intervall1                                |
| Grunnlag for eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonKontrollOverStemmerettigheter.grunnlag                                                        | grunnlagstype.indirekte                                        |
| Mellomliggende virksomhet                                                        | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonKontrollOverStemmerettigheter.mellomliggendeVirksomhet[0].erUtenlandskVirksomhet              | false                                                          |
| Organisasjonsnummer til Woods AS                                                 | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonKontrollOverStemmerettigheter.mellomliggendeVirksomhet[0].norskVirksomhet.organisasjonsnummer | 310274682                                                      |
| *Hilde Knutsen*                                                                  |                                                                                                                                                        |                                                                |
| Er personen registrert i folkeregisteret                                         | skjemainnhold.skjemadata.reellRettighetshaver[2].erRegistrertIFolkeregisteret                                                                          | true                                                           |
| Fødselsnummer                                                                    | skjemainnhold.skjemadata.reellRettighetshaver[2].folkeregistrertPerson.foedselsEllerDNummer                                                            | 06909997850                                                    |
| Har posisjon eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonEierskap                                                                                   | false                                                          |
| Har posisjon kontroll over stemmerettigheter                                     | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonKontrollOverStemmerettigheter                                                              | false                                                          |
| Har posisjon kontroll på annen måte                                              | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonKontrollPaaAnnenMaate                                                                      | false                                                          |
| Har posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene                                | true                                                           |
| Har posisjon avgitt grunnkapital                                                 | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonAvgittGrunnkapital                                                                         | false                                                          |
| Har posisjon rett til å utpeke et flertall av styremedlemmene                    | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene                                                 | false                                                          |
| Har posisjon destinatar                                                          | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonDestinatar                                                                                 | false                                                          |
| Har posisjon særlige rettigheter                                                 | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonSaerligeRettigheter                                                                        | false                                                          |
| Grunnlag for posisjon                                                            | skjemainnhold.skjemadata.reellRettighetshaver[2].grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene                      | grunnlagstype.enighetEllerAvtale                               |
| *Bente Hansen*                                                                   |                                                                                                                                                        |                                                                |
| Er personen registrert i folkeregisteret                                         | skjemainnhold.skjemadata.reellRettighetshaver[3].erRegistrertIFolkeregisteret                                                                          | true                                                           |
| Fødselsnummer                                                                    | skjemainnhold.skjemadata.reellRettighetshaver[3].folkeregistrertPerson.foedselsEllerDNummer                                                            | 13853448138                                                    |
| Har posisjon eierskap                                                            | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonEierskap                                                                                   | false                                                          |
| Har posisjon kontroll over stemmerettigheter                                     | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonKontrollOverStemmerettigheter                                                              | false                                                          |
| Har posisjon kontroll på annen måte                                              | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonKontrollPaaAnnenMaate                                                                      | true                                                           |
| Har posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene                                | false                                                          |
| Har posisjon avgitt grunnkapital                                                 | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonAvgittGrunnkapital                                                                         | false                                                          |
| Har posisjon rett til å utpeke et flertall av styremedlemmene                    | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene                                                 | false                                                          |
| Har posisjon destinatar                                                          | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonDestinatar                                                                                 | false                                                          |
| Har posisjon særlige rettigheter                                                 | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonSaerligeRettigheter                                                                        | false                                                          |
| Posisjon kontroll på en annen måte beskrivelse                                   | skjemainnhold.skjemadata.reellRettighetshaver[3].beskrivelseAvPosisjonenKontrollPaaAnnenMaate                                                          | Verge for en mindreårig aksjeeier som eier 40% av aksjene      |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
  "versjon": "1.0.0",
  "endret": "2024-08-12",
  "skjemainnhold": {
    "metadata": {
      "tjeneste": "rrh.ktr.reelle",
      "tjenestehandling": "nyregistrering",
      "rettighetsinformasjonsid": "RRH202400000193",
      "registreringsid": "2cf3cc0e-f11d-446c-ac67-8e35c6c7b8c2"
    },
    "fagsystem": {
      "organisasjonsnummer": null,
      "navn": null
    },
    "integrasjon": {
      "hfHentPreutfyllingFeilet": false,
      "hfHentRollerFeilet": null
    },
    "skjemadata": {
      "registreringspliktigVirksomhet": {
        "organisasjonsnummer": "313164926",
        "hfSoekOrganisasjonsnummerFeilkode": null,
        "hfNavn": "Snekkeren AS",
        "hfOrganisasjonsform": "AS",
        "hfForretningsadresse": null,
        "hfNavnPaaHovedvirksomhetRegistrertIEoes": null,
        "hfLandnavnForHovedvirksomhetRegistrertIEoes": null,
        "hfSoekPaaOrganisasjonsnummer": null
      },
      "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
      "aarsakTilAtVirksomhetIkkeHarReelleRettighetshavere": null,
      "finnesDetReelleRettighetshavereITilleggTilRolleinnehavereForStiftelse": null,
      "reellRettighetshaver": [
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "41864000647"
          },
          "harPosisjonEierskap": true,
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonKontrollPaaAnnenMaate": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false,
          "posisjonEierskap": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall1",
            "grunnlag": "grunnlagstype.direkte"
          }
        },
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "27899995479"
          },
          "harPosisjonEierskap": false,
          "harPosisjonKontrollOverStemmerettigheter": true,
          "harPosisjonKontrollPaaAnnenMaate": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false,
          "posisjonKontrollOverStemmerettigheter": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall1",
            "grunnlag": "grunnlagstype.indirekte",
            "mellomliggendeVirksomhet": [
              {
                "erUtenlandskVirksomhet": false,
                "norskVirksomhet": {
                  "organisasjonsnummer": "310274682"
                }
              }
            ]
          }
        },
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "06909997850"
          },
          "harPosisjonEierskap": false,
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonKontrollPaaAnnenMaate": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": true,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false,
          "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": "grunnlagstype.enighetEllerAvtale"
        },
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "13853448138"
          },
          "harPosisjonEierskap": false,
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonKontrollPaaAnnenMaate": true,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false,
          "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": "Verge for en mindreårig aksjeeier som eier 40% av aksjene"
        }
      ],
      "kanIkkeIdentifisereFlereReelleRettighetshavere": false,
      "erVirksomhetRegistrertPaaRegulertMarked": null,
      "regulertMarked": null,
      "erReelleRettighetshavereRegistrertIUtenlandskRegister": null,
      "utenlandskRegister": null,
      "rolleinnehaver": null
    }
  }
}
{{< /expandableCode >}}

## Eksempel 5: Fem reelle rettighetshavere som eier 20% hver

Snekkeren AS har fått melding i Altinn fra Register over reelle rettighetshavere om at virksomheten må registrere sine
reelle rettighetshavere. Virksomheten benytter et sluttbrukersystem som tilbyr en løsning for maskinell
innrapportering. Ole Olsen, Svante Sturesson, Bente Hansen, Hilde Knutsen og Sølvi Person eier 20% hver av aksjene i
Snekkeren AS. Ingen eier over 25% av virksomheten og det foreligger ingen interne avtaler som gjør at noen har større 
stemmerett enn andre aksjeeiere. Av den grunn skal virksomheten registrere at de ikke har reelle rettighetshavere.
En av de som har tilgang logger seg inn på sitt sluttbrukersystem, sørger for å rapportere for Snekkeren AS, og sender
inn opplysninger om reelle rettighetshavere.

| Opplysninger som skal sendes inn                              | JSON-sti                                                                                                               | JSON-verdi                                                         |
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| Virksomhetens organisasjonsnummer                             | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                                            | 312962012                                                          |
| Har virksomheten reelle rettighetshavere                      | skjemainnhold.skjemadata.reelleRettighetshavereidentifikasjon                                                          | reellerettighetshavereidentifikasjon.harIkkeReelleRettighetshavere |
| Er eid eller kontrollert av offentlig virksomhet              | skjemainnhold.skjemadata.aarsakTilAtVirksomhetIkkeHarReelleRettighetshavere.erEidEllerKontrollertAvOffentligVirksomhet | false                                                              |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
  "versjon": "1.0.0",
  "endret": "2024-08-12",
  "skjemainnhold": {
    "metadata": {
      "tjeneste": "rrh.ktr.reelle",
      "tjenestehandling": "nyregistrering",
      "rettighetsinformasjonsid": "RRH202400000192",
      "registreringsid": "7c42543e-89b8-4b00-aa03-586ec98edece"
    },
    "fagsystem": {
      "organisasjonsnummer": null,
      "navn": null
    },
    "integrasjon": {
      "hfHentPreutfyllingFeilet": false,
      "hfHentRollerFeilet": null
    },
    "skjemadata": {
      "registreringspliktigVirksomhet": {
        "organisasjonsnummer": "312962012",
        "hfSoekOrganisasjonsnummerFeilkode": null,
        "hfNavn": "Snekkeren AS",
        "hfOrganisasjonsform": "AS",
        "hfForretningsadresse": null,
        "hfNavnPaaHovedvirksomhetRegistrertIEoes": null,
        "hfLandnavnForHovedvirksomhetRegistrertIEoes": null,
        "hfSoekPaaOrganisasjonsnummer": null
      },
      "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harIkkeReelleRettighetshavere",
      "aarsakTilAtVirksomhetIkkeHarReelleRettighetshavere": {
        "erEidEllerKontrollertAvOffentligVirksomhet": false,
        "erOffentligVirksomhetUtenlandsk": null
      },
      "finnesDetReelleRettighetshavereITilleggTilRolleinnehavereForStiftelse": null,
      "reellRettighetshaver": [],
      "kanIkkeIdentifisereFlereReelleRettighetshavere": null,
      "erVirksomhetRegistrertPaaRegulertMarked": null,
      "regulertMarked": null,
      "erReelleRettighetshavereRegistrertIUtenlandskRegister": null,
      "utenlandskRegister": null,
      "rolleinnehaver": null
    }
  }
}
{{< /expandableCode >}}