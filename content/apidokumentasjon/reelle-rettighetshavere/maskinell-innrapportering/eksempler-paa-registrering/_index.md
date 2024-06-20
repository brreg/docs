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

Ole Olsen er eneaksjonær i Snekkeren AS, og har fått brev fra Register over reelle rettighetshavere om at virksomheten må registrere sine reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell innrapportering.

### Hva skal virksomheten gjøre?

Ole Olsen logger seg inn på sitt sluttbrukersystem, sørger for at han rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere. Han skal fylle ut følgende:

* Virksomheten har reelle rettighetshavere
* Oppgi fødselsnummer til Ole Olsen
* 75% - 100% eierskap
* Grunnlag for eierskapet er direkte
* Mangler ikke opplysninger for å kunne identifisere noen av virksomhetens reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}

## Eksempel 2: To reelle rettighetshavere i et AS, en norsk og en utenlandsk {#eksempel2}

### Brukerreise
Ole Olsen og Svante Turesson (er svensk, men har både svensk og amerikansk statsborgerskap) eier 50% hver i Snekkeren AS, og virksomheten har fått brev fra Register over reelle rettighetshavere om at virksomheten må registrere sine reelle rettighetshavere. Virksomheten har et sluttbrukersystem som har implementert muligheter for maskinell innrapportering.

### Hva skal virksomheten gjøre?
Ole Olsen eller Gill Bates logger seg inn på sitt sluttbrukersystem, sørger for at de rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere. De skal fylle ut følgende før innsending:

* Virksomheten har reelle rettighetshavere
* Oppgi fødselsnummer til Ole Olsen
* Personen eier 50% - 74,99% av virksomheten
* Grunnlag for eierskapet er direkte
* Fødselsdato for Svante Turesson
* Fullt navn
* Bostedsland "Sverige"
* "Sverige" og "USA" som statsborgerskap
* Personen eier 50% - 74,99% av virksomheten
* Grunnlag for eierskapet er direkte
* Mangler ikke opplysninger for å kunne identifisere noen av virksomhetens reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}

## Eksempel 3: En reell rettighetshaver med to mellomliggende virksomheter (norsk og utenlandsk) {#eksempel3}
### Brukerreise
Ole Olsen er indirekte eier i Snekkeren AS fordi han eier 60% av aksjene i både Trelast AS og Woods AB. Resterende 40 % av aksjene i virksomhetene er eid av ansatte som har under 25 % hver.

### Hva skal virksomheten gjøre?
Ole Olsen logger seg inn på sitt sluttbrukersystem, sørger for at han rapporterer for Snekkeren AS, og finner innsending av reelle rettighetshavere. Han skal fylle ut følgende:

* Virksomheten har reelle rettighetshavere
* Oppgi fødselsnummer til Ole Olsen
* Personen eier 50% - 74,99% virksomheten
* Grunnlag for eierskapet er indirekte
* Norsk virksomhet
* Organisasjonsnummer til Trelast AS
* Utenlandsk virksomhet
* Navn på utenlandsk  virksomhet, Woods AB
* Evt. registreringsnummer i hjemland
* Adresse
* Land
* Mangler ikke opplysninger for å kunne identifisere noen av virksomhetens reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}


## Eksempel 4: Fire reelle rettighetshavere med hver sin posisjon {#eksempel4}
### Brukerreise
### Hva skal virksomheten gjøre?
{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}


## Eksempel 5: Fem reelle rettighetshavere som eier 20% hver {#eksempel5}
### Brukerreise
Ole Olsen, Svante Sturesson, Bente Hansen, Hilde Knutsen og Sølvi Person eier 20% hver av aksjene i Snekkeren AS, og det foreligger ingen interne avtaler som gjør at noen av dem har større stemmerett enn andre aksjeeiere.

### Hva skal virksomheten gjøre?
En av de som har tilgang til virksomheten sitt sluttbrukersystem logger seg inn, sørger for at han/hun rapporterer for Snekkeren AS, finner innsending av reelle rettighetshavere, og fyller ut følgende:

* Virksomheten har ikke reelle rettighetshavere

{{< expandableCode title="JSON-eksempel" lang="json" >}}
{
    "eksempel": "kommer"
}
{{< /expandableCode >}}
