---
title: Eksempler på en registrering
description: Eksempler på hvordan en registrering kan se ut
weight: 200
---

<!-- TOC -->
* [Eksempel 1: Eneaksjonær i et AS](#eksempel1)
* [Eksempel 2: To reelle rettighetshavere i et AS, en norsk og en utenlandsk](#eksempel2)
* [Eksempel 3: En reell rettighetshaver med to mellomliggende virksomheter (norsk og utenlandsk)](#eksempel3)
* [Eksempel 4: Fire reelle rettighetshavere med hver sin posisjon](#eksempel4)
* [Eksempel 5: Fem reelle rettighetshavere som eier 20% hver](#eksempel5)
<!-- TOC -->

## Eksempel 1: Eneaksjonær i et AS {#eksempel1}

### Brukerreise

Ole Olsen er eneaksjonær i Snekkeren AS, og har fått brev fra Register over reelle rettighetshavere om at virksomheten må registrere sine reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell innrapportering. Ole Olsen logger seg inn på sitt sluttbrukersystem, sørger for at han rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere.

### Hva skal virksomheten registrere?

* virksomheten har reelle rettighetshavere
* oppgi fødselsnummer til Ole Olsen
* 75% - 100% eierskap
* grunnlag for eierskapet er direkte
* mangler ikke opplysninger for å kunne identifisere noen av virksomhetens reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
  "skjemadata": {
    "registreringspliktigVirksomhet": {
      "organisasjonsnummer": "313976769"
    },
    "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
    "aarsakTilAtVirksomhetIkkeHarReelleRettighetshavere": null,
    "finnesDetReelleRettighetshavereITilleggTilRolleinnehavereForStiftelse": null,
    "reellRettighetshaver": [
      {
        "erRegistrertIFolkeregisteret": true,
        "folkeregistrertPerson": {
          "foedselsEllerDNummer": "20825796305"
        },
        "utenlandskPerson": null,
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
        "harPosisjonSaerligeRettigheter": false
      }
    ],
    "kanIkkeIdentifisereFlereReelleRettighetshavere": false,
    "erVirksomhetRegistrertPaaRegulertMarked": null,
    "regulertMarked": null,
    "erReelleRettighetshavereRegistrertIUtenlandskRegister": null,
    "utenlandskRegister": null,
    "rolleinnehaver": []
  }
}
{{< /expandableCode >}}

## Eksempel 2: To reelle rettighetshavere i et AS, en norsk og en utenlandsk {#eksempel2}

### Brukerreise
Ole Olsen og Svante Turesson (er svensk, men har både svensk og amerikansk statsborgerskap) eier 50% hver i Snekkeren AS, og virksomheten har fått brev fra Register over reelle rettighetshavere om at virksomheten må registrere sine reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell innrapportering. Ole Olsen eller Gill Bates logger seg inn på sitt sluttbrukersystem, sørger for at de rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere.

### Hva skal virksomheten registrere?

* virksomheten har reelle rettighetshavere
* oppgi fødselsnummer til Ole Olsen
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

## Eksempel 3: En reell rettighetshaver med to mellomliggende virksomheter (norsk og utenlandsk) {#eksempel3}

### Brukerreise
Ole Olsen er indirekte eier i Snekkeren AS fordi han eier 60% av aksjene i både Trelast AS og Woods AB. Resterende 40 % av aksjene i virksomhetene er eid av ansatte som har under 25 % hver. Ole Olsen logger seg inn på sitt sluttbrukersystem, sørger for at han rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere.

### Hva skal virksomheten registrere?

* virksomheten har reelle rettighetshavere
* oppgi fødselsnummer til Ole Olsen
* personen eier 50% - 74,99% virksomheten
* grunnlag for eierskapet er indirekte
* norsk virksomhet
* organisasjonsnummer til Trelast AS
* utenlandsk virksomhet
* navn på utenlandsk  virksomhet, Woods AB
* evt registreringsnummer i hjemland
* adresse
* land
* mangler ikke opplysninger for å kunne identifisere noen av virksomhetens reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}


## Eksempel 4: Fire reelle rettighetshavere med hver sin posisjon {#eksempel4}

### Brukerreise
Snekkeren AS har fire reelle rettighetshavere som har hver sin posisjon. Ole Olsen eier 26% av aksjene, Hans Hansen eier 20% av aksjene, men har 28% stemmerettighet fordi han eier 28% av Woods AS, Hilde Knutsen eier 10% av virksomheten, men har en intern avtale som gjør at hun har rett til å utpeke eller avsette mer enn halvparten av styremedlemmer, Bente Hansen er verge for en mindreårig aksjeeier som eier 40% av aksjene.

### Hva skal virksomheten registrere?

* virksomheten har reelle rettighetshavere
* oppgi fødselsnummer til Ole Olsen
* personen eier 25,01% - 49,99% av virksomheten
* grunnlag for eierskapet er direkte
* oppgi fødselsnummer til Hans Hansen
* personen har kontroll over stemmerettighet på 25,01% - 49,99%
* grunnlag for stemmerettighet er indirekte
* organisasjonsnummer på mellomliggende virksomhet
* oppgi fødselsnummer til Hilde Knutsen
* har rett til å utpeke eller avsette mer enn halvparten av styremedlemmer
* grunnlag etter enighet eller avtale
* oppgi fødselsnummer til Bente Hansen
* skriv forklaring i feltet Posisjon kontroll på annen måte

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}


## Eksempel 5: Fem reelle rettighetshavere som eier 20% hver {#eksempel5}
### Brukerreise
Ole Olsen, Svante Sturesson, Bente Hansen, Hilde Knutsen og Sølvi Person eier 20% hver av aksjene i Snekkeren AS, og det foreligger ingen interne avtaler som gjør at noen av dem har større stemmerett enn andre aksjeeiere. En av de som har tilgang til virksomheten sitt sluttbrukersystem logger seg inn, sørger for at han/hun rapporterer for Snekkeren AS, finner innsending av reelle rettighetshavere.

### Hva skal virksomheten gjøre?
* virksomheten har ikke reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}