---
title: Eksempler
description: Eksempler på hvordan en registrering kan se ut
weight: 200
---

<!-- TOC -->
  * [Eksempel 1: Eneaksjonær i et AS](#eksempel-1-eneaksjonær-i-et-as)
    * [Brukerreise](#brukerreise)
    * [Hvilke opplysninger skal sendes inn?](#hvilke-opplysninger-skal-sendes-inn)
  * [Eksempel 2: To reelle rettighetshavere i et AS, en norsk og en utenlandsk](#eksempel-2-to-reelle-rettighetshavere-i-et-as-en-norsk-og-en-utenlandsk)
    * [Brukerreise](#brukerreise-1)
    * [Hvilke opplysninger skal sendes inn?](#hvilke-opplysninger-skal-sendes-inn-1)
  * [Eksempel 3: En reell rettighetshaver med en mellomliggende virksomhet](#eksempel-3-en-reell-rettighetshaver-med-en-mellomliggende-virksomhet)
    * [Brukerreise](#brukerreise-2)
    * [Hvilke opplysninger skal sendes inn?](#hvilke-opplysninger-skal-sendes-inn-2)
  * [Eksempel 4: Fire reelle rettighetshavere med hver sin posisjon](#eksempel-4-fire-reelle-rettighetshavere-med-hver-sin-posisjon)
    * [Brukerreise](#brukerreise-3)
    * [Hvilke opplysninger skal sendes inn?](#hvilke-opplysninger-skal-sendes-inn-3)
  * [Eksempel 5: Fem reelle rettighetshavere som eier 20% hver](#eksempel-5-fem-reelle-rettighetshavere-som-eier-20-hver)
    * [Brukerreise](#brukerreise-4)
    * [Hvilke opplysninger skal sendes inn?](#hvilke-opplysninger-skal-sendes-inn-4)
<!-- TOC -->

## Eksempel 1: Eneaksjonær i et AS

### Brukerreise

Ole Olsen er eneaksjonær i Snekkeren AS, og har fått brev fra Register over reelle rettighetshavere om at virksomheten 
må registrere sine reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for 
maskinell innrapportering. Ole Olsen logger seg inn på sitt sluttbrukersystem, sørger for at han rapporterer for 
Snekkeren AS, og finner innsending av reelle rettighetshavere.

### Hvilke opplysninger skal sendes inn?

* virksomheten har reelle rettighetshavere
* fødselsnummer til Ole Olsen
* 75% - 100% eierskap
* grunnlag for eierskapet er direkte
* mangler ikke opplysninger for å kunne identifisere noen av virksomhetens reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
  "versjon": "0.0.7",
  "endret": "2024-05-07",
  "skjemainnhold": {
    "metadata": {
      "tjeneste": "rrh.ktr.reelle",
      "tjenestehandling": "endring",
      "rettighetsinformasjonsid": "RRH202300000020",
      "registreringsid": "cace0a64-cf41-4c33-af37-a6f16aa9e356"
    },
    "fagsystem": {
      "organisasjonsnummer": "313496058",
      "navn": "Sluttbrukersystem sitt navn"
    },
    "skjemadata": {
      "registreringspliktigVirksomhet": {
        "organisasjonsnummer": "311780352"
      },
      "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
      "reellRettighetshaver": [
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "05910298382"
          },
          "harPosisjonEierskap": true,
          "posisjonEierskap": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall3",
            "grunnlag": "grunnlagstype.direkte",
            "mellomliggendeVirksomhet": []
          },
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false
        }
      ],
      "kanIkkeIdentifisereFlereReelleRettighetshavere": false,
      "rolleinnehaver": []
    }
  }
}
{{< /expandableCode >}}

## Eksempel 2: To reelle rettighetshavere i et AS, en norsk og en utenlandsk

### Brukerreise
Ole Olsen og Svante Turesson (er svensk, men har både svensk og amerikansk statsborgerskap) eier 50% hver i 
Snekkeren AS, og virksomheten har fått brev fra Register over reelle rettighetshavere om at virksomheten må registrere 
sine reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell 
innrapportering. Ole Olsen eller Gill Bates logger seg inn på sitt sluttbrukersystem, sørger for at de rapporterer 
for Snekkeren AS, og finner innsending av reelle rettighetshavere.

### Hvilke opplysninger skal sendes inn?

* virksomheten har reelle rettighetshavere
* fødselsnummer til Ole Olsen
* personen eier 50% - 74,99% av virksomheten
* grunnlag for eierskapet er direkte
* fødselsdato for Svante Turesson
* fullt navn
* bostedsland "Sverige"
* "Sverige" og "USA" som statsborgerskap
* personen eier 50% - 74,99% av virksomheten
* grunnlag for eierskapet er direkte
* mangler ikke opplysninger for å kunne identifisere noen av virksomhetens reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}

## Eksempel 3: En reell rettighetshaver med en mellomliggende virksomhet

### Brukerreise
Ole Olsen er indirekte eier i Snekkeren AS fordi han eier 60% av aksjene i Trelast AS. Resterende 40 % av aksjene i 
virksomhetene er eid av ansatte som har under 25 % hver. Ole Olsen logger seg inn på sitt sluttbrukersystem, sørger for 
at han rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere.


### Hvilke opplysninger skal sendes inn?

* virksomheten har reelle rettighetshavere
* fødselsnummer til Ole Olsen
* personen eier 50% - 74,99% virksomheten
* grunnlag for eierskapet er indirekte
* norsk virksomhet
* organisasjonsnummer til Trelast AS
* mangler ikke opplysninger for å kunne identifisere noen av virksomhetens reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
  "versjon": "0.0.7",
  "endret": "2024-05-07",
  "skjemainnhold": {
    "metadata": {
      "tjeneste": "rrh.ktr.reelle",
      "tjenestehandling": "endring",
      "rettighetsinformasjonsid": "RRH202300000010",
      "registreringsid": "8394533b-9d2b-43a4-a4c5-5fb8ce6ca3a5"
    },
    "fagsystem": {
      "organisasjonsnummer": "313496058",
      "navn": "Sluttbrukersystem sitt navn"
    },
    "skjemadata": {
      "registreringspliktigVirksomhet": {
        "organisasjonsnummer": "314208641"
      },
      "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
      "reellRettighetshaver": [
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "41864000647"
          },
          "harPosisjonEierskap": true,
          "posisjonEierskap": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall2",
            "grunnlag": "grunnlagstype.indirekte",
            "mellomliggendeVirksomhet": [
              {
                "erUtenlandskVirksomhet": false,
                "norskVirksomhet": {
                  "organisasjonsnummer": "313513408"
                }
              }
            ]
          },
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false
        }
      ],
      "kanIkkeIdentifisereFlereReelleRettighetshavere": false,
      "rolleinnehaver": []
    }
  }
}
{{< /expandableCode >}}


## Eksempel 4: Fire reelle rettighetshavere med hver sin posisjon

### Brukerreise
Snekkeren AS har fire reelle rettighetshavere som har hver sin posisjon. Ole Olsen eier 26% av aksjene, Hans Hansen 
eier 20% av aksjene, men har 28% stemmerettighet fordi han eier 28% av Woods AS, Hilde Knutsen eier 10% av 
virksomheten, men har en intern avtale som gjør at hun har rett til å utpeke eller avsette mer enn halvparten av 
styremedlemmer, Bente Hansen er verge for en mindreårig aksjeeier som eier 40% av aksjene. En av de som har tilgang 
logger seg inn på sitt sluttbrukersystem, sørger for at de rapporterer for Snekkeren AS, og finner innsending av reelle 
rettighetshavere.

### Hvilke opplysninger skal sendes inn?

* virksomheten har reelle rettighetshavere
* fødselsnummer til Ole Olsen
* personen eier 25,01% - 49,99% av virksomheten
* grunnlag for eierskapet er direkte
* fødselsnummer til Hans Hansen
* personen har kontroll over stemmerettighet på 25,01% - 49,99%
* grunnlag for stemmerettighet er indirekte
* organisasjonsnummer på mellomliggende virksomhet
* fødselsnummer til Hilde Knutsen
* har rett til å utpeke eller avsette mer enn halvparten av styremedlemmer
* grunnlag etter enighet eller avtale
* fødselsnummer til Bente Hansen
* skriv forklaring i feltet Posisjon kontroll på annen måte

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}


## Eksempel 5: Fem reelle rettighetshavere som eier 20% hver
### Brukerreise
Ole Olsen, Svante Sturesson, Bente Hansen, Hilde Knutsen og Sølvi Person eier 20% hver av aksjene i Snekkeren AS, og 
det foreligger ingen interne avtaler som gjør at noen av dem har større stemmerett enn andre aksjeeiere. En av de som 
har tilgang til virksomheten sitt sluttbrukersystem logger seg inn, sørger for at han/hun rapporterer for Snekkeren AS, 
finner innsending av reelle rettighetshavere. En av de som har tilgang logger seg inn på sitt sluttbrukersystem, sørger 
for at de rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere.

### Hvilke opplysninger skal sendes inn?
* virksomheten har ikke reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}