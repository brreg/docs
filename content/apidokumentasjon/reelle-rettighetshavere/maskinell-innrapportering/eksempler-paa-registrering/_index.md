---
title: Eksempler
description: Eksempler på hvordan en registrering kan se ut
weight: 200
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

| Opplysninger som skal sendes inn         | JSON-sti                                                                                    | JSON-verdi                                                     |
|------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Virksomhetens organisasjonsnummer        | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                 | 310956643                                                      |
| Har virksomheten reelle rettighetshavere | skjemainnhold.skjemadata.reelleRettighetsregistreringspliktigVirksomhethavereidentifikasjon | reellerettighetshavereidentifikasjon.harReelleRettighetshavere |
| *Ole Olsen*                              |                                                                                             |                                                                |
| Er personen registrert i folkeregisteret | skjemainnhold.skjemadata.reellRettighetshaver[0].erRegistrertIFolkeregisteret               | true                                                           |
| Fødselsnummer                            | skjemainnhold.skjemadata.reellRettighetshaver[0].folkeregistrertPerson.foedselsEllerDNummer | 41864000647                                                    |
| Har posisjon eierskap                    | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonEierskap                        | true                                                           |
| Eierskap størrelsesintervall 75% - 100%  | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.stoerrelsesintervall      | stoerrelsesintervall.intervall3                                |
| Grunnlag for eierskap                    | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.grunnlag                  | grunnlagstype.direkte                                          |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "versjon": "1.0.0",
    "endret": "2024-08-12",
    "skjemainnhold": {
        "metadata": {
            "tjeneste": "rrh.ktr.reelle",
            "tjenestehandling": "endring",
            "rettighetsinformasjonsid": "RRH202400000182",
            "registreringsid": "daa79643-f763-4be6-8a8b-5ef93e2c5bec"
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
                "organisasjonsnummer": "310956643",
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
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": {
                        "foedselsEllerDNummer": "41864000647",
                        "hfFulltNavn": "Ole Olsen",
                        "hfBostedsland": "UKJENT",
                        "hfStatsborgerskap": "Norge",
                        "hfSoekPaaEtternavn": null,
                        "hfSoekFeilkode": null,
                        "hfSoekPaaFoedselsEllerDNummer": null
                    },
                    "utenlandskPerson": null,
                    "hfFulltNavnTabellvisning": "Ole Olsen",
                    "harPosisjonEierskap": true,
                    "posisjonEierskap": {
                        "stoerrelsesintervall": "stoerrelsesintervall.intervall3",
                        "grunnlag": "grunnlagstype.direkte",
                        "mellomliggendeVirksomhet": []
                    },
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": null,
                    "harPosisjonKontrollPaaAnnenMaate": null,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": null,
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Eierskap 75% - 100%"
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
reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell
innrapportering. Ole Olsen og Svante Turesson (er svensk, men har både svensk og amerikansk statsborgerskap) eier 50%
hver i Snekkeren AS. Ole Olsen eller Svante Turesson logger seg inn på sitt sluttbrukersystem, sørger for at de
rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere.

| Opplysninger som skal sendes inn           | JSON-sti                                                                                    | JSON-verdi                                                     |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Virksomhetens organisasjonsnummer          | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                 | 310956643                                                      |
| Har virksomheten reelle rettighetshavere   | skjemainnhold.skjemadata.reelleRettighetsregistreringspliktigVirksomhethavereidentifikasjon | reellerettighetshavereidentifikasjon.harReelleRettighetshavere |
| *Ole Olsen*                                |                                                                                             |                                                                |
| Er personen registrert i folkeregisteret   | skjemainnhold.skjemadata.reellRettighetshaver[0].erRegistrertIFolkeregisteret               | true                                                           |
| Fødselsnummer                              | skjemainnhold.skjemadata.reellRettighetshaver[0].folkeregistrertPerson.foedselsEllerDNummer | 41864000647                                                    |
| Har posisjon eierskap                      | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonEierskap                        | true                                                           |
| Eierskap størrelsesintervall  50% - 74,99% | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.stoerrelsesintervall      | stoerrelsesintervall.intervall2                                |
| Grunnlag for eierskap                      | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.grunnlag                  | grunnlagstype.direkte                                          |
| *Svante Turesson*                          |                                                                                             |                                                                |
| Er personen registrert i folkeregisteret   | skjemainnhold.skjemadata.reellRettighetshaver[1].erRegistrertIFolkeregisteret               | false                                                          |
| Fødselsdato for                            | skjemainnhold.skjemadata.reellRettighetshaver[1].utenlandskPerson.foedselsdato              | 1982-01-01                                                     |
| Fullt navn                                 | skjemainnhold.skjemadata.reellRettighetshaver[1].utenlandskPerson.fulltNavn                 | Svante Turesson                                                |
| Bostedsland: Servige                       | skjemainnhold.skjemadata.reellRettighetshaver[1].utenlandskPerson.bostedsland               | SWE                                                            |
| Statsborgerskap: Sverige og USA            | skjemainnhold.skjemadata.reellRettighetshaver[1].utenlandskPerson.statsborgerskap           | SWE,USA                                                        |
| Har posisjon eierskap                      | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonEierskap                        | true                                                           |
| Eierskap størrelsesintervall  50% - 74,99% | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.stoerrelsesintervall      | stoerrelsesintervall.intervall2                                |
| Grunnlag for eierskap                      | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.grunnlag                  | grunnlagstype.direkte                                          |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "versjon": "1.0.0",
    "endret": "2024-08-12",
    "skjemainnhold": {
        "metadata": {
            "tjeneste": "rrh.ktr.reelle",
            "tjenestehandling": "endring",
            "rettighetsinformasjonsid": "RRH202400000182",
            "registreringsid": "9da10db1-15bd-4067-82eb-33f347ba9c2f"
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
                "organisasjonsnummer": "310956643",
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
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": {
                        "foedselsEllerDNummer": "41864000647",
                        "hfFulltNavn": "Ole Olsen",
                        "hfBostedsland": "UKJENT",
                        "hfStatsborgerskap": "Norge",
                        "hfSoekPaaEtternavn": null,
                        "hfSoekFeilkode": null,
                        "hfSoekPaaFoedselsEllerDNummer": null
                    },
                    "utenlandskPerson": null,
                    "hfFulltNavnTabellvisning": "Ole Olsen",
                    "harPosisjonEierskap": true,
                    "posisjonEierskap": {
                        "stoerrelsesintervall": "stoerrelsesintervall.intervall2",
                        "grunnlag": "grunnlagstype.direkte",
                        "mellomliggendeVirksomhet": []
                    },
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": null,
                    "harPosisjonKontrollPaaAnnenMaate": null,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": null,
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Eierskap 50% - 74,99%"
                },
                {
                    "erRegistrertIFolkeregisteret": false,
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": null,
                    "utenlandskPerson": {
                        "foedselsdato": "1982-01-01",
                        "fulltNavn": "Svante Turesson",
                        "bostedsland": "SWE",
                        "statsborgerskap": "SWE,USA"
                    },
                    "hfFulltNavnTabellvisning": "Svante Turesson",
                    "harPosisjonEierskap": true,
                    "posisjonEierskap": {
                        "stoerrelsesintervall": "stoerrelsesintervall.intervall2",
                        "grunnlag": "grunnlagstype.direkte",
                        "mellomliggendeVirksomhet": []
                    },
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": null,
                    "harPosisjonKontrollPaaAnnenMaate": null,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": null,
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Eierskap 50% - 74,99%"
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
reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell
innrapportering. Ole Olsen er indirekte eier i Snekkeren AS fordi han eier 100% av aksjene i Trelast AS, som igjen eier
60% av aksjene i Snekkeren AS. Resterende 40 % av aksjene i Snekkeren AS er eid av ansatte som har under 25 % hver.
Ole Olsen logger seg inn på sitt sluttbrukersystem, sørger for han rapporterer for Snekkeren AS, og finner innsending
av reelle rettighetshavere.

| Opplysninger som skal sendes inn           | JSON-sti                                                                                                                          | JSON-verdi                                                     |
|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Virksomhetens organisasjonsnummer          | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                                                       | 310956643                                                      |
| Har virksomheten reelle rettighetshavere   | skjemainnhold.skjemadata.reelleRettighetsregistreringspliktigVirksomhethavereidentifikasjon                                       | reellerettighetshavereidentifikasjon.harReelleRettighetshavere |
| *Ole Olsen*                                |                                                                                                                                   |                                                                |
| Er personen registrert i folkeregisteret   | skjemainnhold.skjemadata.reellRettighetshaver[0].erRegistrertIFolkeregisteret                                                     | true                                                           |
| Fødselsnummer                              | skjemainnhold.skjemadata.reellRettighetshaver[0].folkeregistrertPerson.foedselsEllerDNummer                                       | 41864000647                                                    |
| Har posisjon eierskap                      | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonEierskap                                                              | true                                                           |
| Eierskap størrelsesintervall  50% - 74,99% | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.stoerrelsesintervall                                            | stoerrelsesintervall.intervall2                                |
| Grunnlag for eierskap                      | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.grunnlag                                                        | grunnlagstype.indirekte                                        |
| Mellomliggende virksomhet                  | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.mellomliggendeVirksomhet[0].erUtenlandskVirksomhet              | false                                                          |
| Organisasjonsnummer til Trelast AS         | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.mellomliggendeVirksomhet[0].norskVirksomhet.organisasjonsnummer | 310219622                                                      |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "versjon": "1.0.0",
    "endret": "2024-08-12",
    "skjemainnhold": {
        "metadata": {
            "tjeneste": "rrh.ktr.reelle",
            "tjenestehandling": "endring",
            "rettighetsinformasjonsid": "RRH202400000182",
            "registreringsid": "95fd1d9a-e335-4787-92ad-fb4951657777"
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
                "organisasjonsnummer": "310956643",
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
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": {
                        "foedselsEllerDNummer": "41864000647",
                        "hfFulltNavn": "Ole Olsen",
                        "hfBostedsland": "UKJENT",
                        "hfStatsborgerskap": "Norge",
                        "hfSoekPaaEtternavn": null,
                        "hfSoekFeilkode": null,
                        "hfSoekPaaFoedselsEllerDNummer": null
                    },
                    "utenlandskPerson": null,
                    "hfFulltNavnTabellvisning": "Ole Olsen",
                    "harPosisjonEierskap": true,
                    "posisjonEierskap": {
                        "stoerrelsesintervall": "stoerrelsesintervall.intervall2",
                        "grunnlag": "grunnlagstype.indirekte",
                        "mellomliggendeVirksomhet": [
                            {
                                "erUtenlandskVirksomhet": false,
                                "norskVirksomhet": {
                                    "organisasjonsnummer": "310219622",
                                    "hfSoekOrganisasjonsnummerFeilkode": null,
                                    "hfNavn": "Trelast AS",
                                    "hfOrganisasjonsform": "Gjensidig forsikringsselskap",
                                    "hfForretningsadresse": "Haldenveien 823, 1892 RAKKESTAD Norge",
                                    "hfNavnPaaHovedvirksomhetRegistrertIEoes": null,
                                    "hfLandnavnForHovedvirksomhetRegistrertIEoes": null,
                                    "hfSoekPaaOrganisasjonsnummer": null
                                },
                                "utenlandskVirksomhet": null,
                                "hfOrganisasjonsnummerEllerRegistreringsnummerIHjemlandet": "310219622",
                                "hfNavn": "Trelast AS",
                                "hfLandnavn": "Norge"
                            }
                        ]
                    },
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": null,
                    "harPosisjonKontrollPaaAnnenMaate": null,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": null,
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Eierskap 50% - 74,99%"
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
reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell
innrapportering. Snekkeren AS har fire reelle rettighetshavere som har hver sin posisjon. Ole Olsen eier 26% av
aksjene, Hans Hansen eier 20% av aksjene, men har 28% stemmerettighet fordi han eier 28% av Woods AS. Woods AS eier 50% 
av Snekkeren AS.  Hilde Knutsen eier 10% av virksomheten, men har en intern avtale som gjør at hun har rett til å utpeke 
eller avsette mer enn halvparten av styremedlemmer, Bente Hansen er verge for en mindreårig aksjeeier som eier 40% av 
aksjene. En av de som har tilgang logger seg inn på sitt sluttbrukersystem, sørger for at de rapporterer for 
Snekkeren AS, og finner innsending av reelle rettighetshavere.

| Opplysninger som skal sendes inn                        | JSON-sti                                                                                                                          | JSON-verdi                                                     |
|---------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Virksomhetens organisasjonsnummer                       | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                                                       | 310956643                                                      |
| Har virksomheten reelle rettighetshavere                | skjemainnhold.skjemadata.reelleRettighetsregistreringspliktigVirksomhethavereidentifikasjon                                       | reellerettighetshavereidentifikasjon.harReelleRettighetshavere |
| *Ole Olsen*                                             |                                                                                                                                   |                                                                |
| Er personen registrert i folkeregisteret                | skjemainnhold.skjemadata.reellRettighetshaver[0].erRegistrertIFolkeregisteret                                                     | true                                                           |
| Fødselsnummer for Ole Olsen                             | skjemainnhold.skjemadata.reellRettighetshaver[0].folkeregistrertPerson.foedselsEllerDNummer                                       | 26920296504                                                    |
| Har posisjon eierskap                                   | skjemainnhold.skjemadata.reellRettighetshaver[0].harPosisjonEierskap                                                              | true                                                           |
| Eierskap størrelsesintervall 25,01% - 49,99%            | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.stoerrelsesintervall                                            | stoerrelsesintervall.intervall1                                |
| Grunnlag for eierskap                                   | skjemainnhold.skjemadata.reellRettighetshaver[0].posisjonEierskap.grunnlag                                                        | grunnlagstype.direkte                                          |
| *Hans Hansen*                                           |                                                                                                                                   |                                                                |
| Er personen registrert i folkeregisteret                | skjemainnhold.skjemadata.reellRettighetshaver[1].erRegistrertIFolkeregisteret                                                     | true                                                           |
| Fødselsnummer                                           | skjemainnhold.skjemadata.reellRettighetshaver[1].folkeregistrertPerson.foedselsEllerDNummer                                       | 27899995479                                                    |
| Har posisjon eierskap                                   | skjemainnhold.skjemadata.reellRettighetshaver[1].harPosisjonEierskap                                                              | true                                                           |
| Stemmerettighet størrelsesintervall 25,01% - 49,99%     | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.stoerrelsesintervall                                            | stoerrelsesintervall.intervall1                                |
| Grunnlag for eierskap                                   | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.grunnlag                                                        | grunnlagstype.indirekte                                        |
| Mellomliggende virksomhet                               | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.mellomliggendeVirksomhet[0].erUtenlandskVirksomhet              | false                                                          |
| Organisasjonsnummer til Woods AS                        | skjemainnhold.skjemadata.reellRettighetshaver[1].posisjonEierskap.mellomliggendeVirksomhet[0].norskVirksomhet.organisasjonsnummer | 310274682                                                      |
| *Hilde Knutsen*                                         |                                                                                                                                   |                                                                |
| Er personen registrert i folkeregisteret                | skjemainnhold.skjemadata.reellRettighetshaver[2].erRegistrertIFolkeregisteret                                                     | true                                                           |
| Fødselsnummer                                           | skjemainnhold.skjemadata.reellRettighetshaver[2].folkeregistrertPerson.foedselsEllerDNummer                                       | 06909997850                                                    |
| Posisjon rett til å utpeke eller avsette styremedlemmer | skjemainnhold.skjemadata.reellRettighetshaver[2].harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene           | true                                                           |
| Grunnlag for posisjon                                   | skjemainnhold.skjemadata.reellRettighetshaver[2].grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene | grunnlagstype.enighetEllerAvtale                               |
| *Bente Hansen*                                          |                                                                                                                                   |                                                                |
| Er personen registrert i folkeregisteret                | skjemainnhold.skjemadata.reellRettighetshaver[3].erRegistrertIFolkeregisteret                                                     | true                                                           |
| Fødselsnummer                                           | skjemainnhold.skjemadata.reellRettighetshaver[3].folkeregistrertPerson.foedselsEllerDNummer                                       | 13853448138                                                    |
| Har posisjon eierskap                                   | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonEierskap                                                              | false                                                          |
| Har posisjon kontroll på en annen måte                  | skjemainnhold.skjemadata.reellRettighetshaver[3].harPosisjonKontrollPaaAnnenMaate                                                 | true                                                           |
| Posisjon kontroll på en annen måte beskrivelse          | skjemainnhold.skjemadata.reellRettighetshaver[3].beskrivelseAvPosisjonenKontrollPaaAnnenMaate                                     | Verge for en mindreårig aksjeeier som eier 40% av aksjene      |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "versjon": "1.0.0",
    "endret": "2024-08-12",
    "skjemainnhold": {
        "metadata": {
            "tjeneste": "rrh.ktr.reelle",
            "tjenestehandling": "endring",
            "rettighetsinformasjonsid": "RRH202400000190",
            "registreringsid": "ff9de949-ecc5-4765-b98f-2eaf03c3467d"
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
                "organisasjonsnummer": "313848981",
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
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": {
                        "foedselsEllerDNummer": "26920296504",
                        "hfFulltNavn": "Ole Olsen",
                        "hfBostedsland": "Norge",
                        "hfStatsborgerskap": "Norge, Uruguay",
                        "hfSoekPaaEtternavn": null,
                        "hfSoekFeilkode": null,
                        "hfSoekPaaFoedselsEllerDNummer": null
                    },
                    "utenlandskPerson": null,
                    "hfFulltNavnTabellvisning": "Ole Olsen",
                    "harPosisjonEierskap": true,
                    "posisjonEierskap": {
                        "stoerrelsesintervall": "stoerrelsesintervall.intervall1",
                        "grunnlag": "grunnlagstype.direkte",
                        "mellomliggendeVirksomhet": []
                    },
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": null,
                    "harPosisjonKontrollPaaAnnenMaate": null,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": null,
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Eierskap 25,01% - 49,99%"
                },
                {
                    "erRegistrertIFolkeregisteret": true,
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": {
                        "foedselsEllerDNummer": "27899995479",
                        "hfFulltNavn": "Hans Hansen",
                        "hfBostedsland": "Norge",
                        "hfStatsborgerskap": "Norge, Kenya",
                        "hfSoekPaaEtternavn": null,
                        "hfSoekFeilkode": null,
                        "hfSoekPaaFoedselsEllerDNummer": null
                    },
                    "utenlandskPerson": null,
                    "hfFulltNavnTabellvisning": "Hans Hansen",
                    "harPosisjonEierskap": true,
                    "posisjonEierskap": {
                        "stoerrelsesintervall": "stoerrelsesintervall.intervall1",
                        "grunnlag": "grunnlagstype.indirekte",
                        "mellomliggendeVirksomhet": [
                            {
                                "erUtenlandskVirksomhet": false,
                                "norskVirksomhet": {
                                    "organisasjonsnummer": "310274682",
                                    "hfSoekOrganisasjonsnummerFeilkode": null,
                                    "hfNavn": "Woods AS",
                                    "hfOrganisasjonsform": "Pensjonskasse",
                                    "hfForretningsadresse": "Kirkebyenga 17A, 2323 HAMAR Norge",
                                    "hfNavnPaaHovedvirksomhetRegistrertIEoes": null,
                                    "hfLandnavnForHovedvirksomhetRegistrertIEoes": null,
                                    "hfSoekPaaOrganisasjonsnummer": null
                                },
                                "utenlandskVirksomhet": null,
                                "hfOrganisasjonsnummerEllerRegistreringsnummerIHjemlandet": "310274682",
                                "hfNavn": "Woods AS",
                                "hfLandnavn": "Norge"
                            }
                        ]
                    },
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": null,
                    "harPosisjonKontrollPaaAnnenMaate": null,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": null,
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Eierskap 25,01% - 49,99%"
                },
                {
                    "erRegistrertIFolkeregisteret": true,
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": {
                        "foedselsEllerDNummer": "06909997850",
                        "hfFulltNavn": "Hilde Knutsen",
                        "hfBostedsland": "Norge",
                        "hfStatsborgerskap": "Norge, Honduras",
                        "hfSoekPaaEtternavn": null,
                        "hfSoekFeilkode": null,
                        "hfSoekPaaFoedselsEllerDNummer": null
                    },
                    "utenlandskPerson": null,
                    "hfFulltNavnTabellvisning": "Hilde Knutsen",
                    "harPosisjonEierskap": false,
                    "posisjonEierskap": null,
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": true,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": "grunnlagstype.enighetEllerAvtale",
                    "harPosisjonKontrollPaaAnnenMaate": null,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": null,
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Avsette eller utpeke styremedlemmer "
                },
                {
                    "erRegistrertIFolkeregisteret": true,
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": {
                        "foedselsEllerDNummer": "13853448138",
                        "hfFulltNavn": "Bente Hansen",
                        "hfBostedsland": "Norge",
                        "hfStatsborgerskap": "El Salvador",
                        "hfSoekPaaEtternavn": null,
                        "hfSoekFeilkode": null,
                        "hfSoekPaaFoedselsEllerDNummer": null
                    },
                    "utenlandskPerson": null,
                    "hfFulltNavnTabellvisning": "Bente Hansen",
                    "harPosisjonEierskap": false,
                    "posisjonEierskap": null,
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": null,
                    "harPosisjonKontrollPaaAnnenMaate": true,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": "Verge for en mindreårig aksjeeier som eier 40% av aksjene",
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Kontroll på annen måte "
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
reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell
innrapportering. Ole Olsen, Svante Sturesson, Bente Hansen, Hilde Knutsen og Sølvi Person eier 20% hver av aksjene i
Snekkeren AS, og det foreligger ingen interne avtaler som gjør at noen har større stemmerett enn andre aksjeeiere.
En av de som har tilgang logger seg inn på sitt sluttbrukersystem, sørger for at de rapporterer for Snekkeren AS, og
finner innsending av reelle rettighetshavere.

| Opplysninger som skal sendes inn         | JSON-sti                                                                                    | JSON-verdi                                                         |
|------------------------------------------|---------------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| Virksomhetens organisasjonsnummer        | skjemainnhold.skjemadata.registreringspliktigVirksomhet.organisasjonsnummer                 | 313848981                                                          |
| Har virksomheten reelle rettighetshavere | skjemainnhold.skjemadata.reelleRettighetsregistreringspliktigVirksomhethavereidentifikasjon | reellerettighetshavereidentifikasjon.harIkkeReelleRettighetshavere |

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "versjon": "1.0.0",
    "endret": "2024-08-12",
    "skjemainnhold": {
        "metadata": {
            "tjeneste": "rrh.ktr.reelle",
            "tjenestehandling": "endring",
            "rettighetsinformasjonsid": "RRH202400000190",
            "registreringsid": "2a0fac7d-c8b9-4279-866d-b717c464195c"
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
                "organisasjonsnummer": "313848981",
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