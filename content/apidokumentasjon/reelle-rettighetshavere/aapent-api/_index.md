---
title: Åpent API
description: Beskrivelse av åpent API for Register over reelle rettighetshavere
weight: 100
---


## Innledning
Brønnøysundregistrene tilbyr en åpen, standardisert maskin-til-maskin-tjeneste (API) som kan benyttes av eksterne konsumenter for innsyn i Register over reelle rettighetshavere.

Denne dokumentasjonen viser hvordan eksterne systemer kan integrere seg mot APIet, og hvordan man benytter seg av tjenesten for å hente data.


***Denne siden er fortsatt under utvikling.***

## API-referanse

Denne tjenesten tilbyr informasjon om reelle rettighetshavere ved oppslag på organisasjonsnummer.

*Lenker til Swagger-dokumentasjon og OpenAPI-spec kommer her.*


## Sikkerhetsmekanismer
Siden dette er et åpent API er det ingen sikkerhetsmekanismer.

## Skjerming

Hvis en reell rettighetshaver er mindreårig eller er unntatt fra innsyn vil enkelte personopplysninger være skjermet.

#### For en skjermet rettighetshaver vil responen kun inneholde:
* foedselsaar
* statsborgerskap
* bostedsland
* posisjon

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                     | Beskrivelse                                                                                                                                                                                      |
|:------------- |:------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/aapen/reelle-rettigheteter/{organisasjonsnummer} | Hent opplysninger om en reell rettighet på angitt organisasjonsnummer. <br/>En reell rettighet for en gitt virksomhet inneholder en liste med reelle rettighetshavere, hvis dette er registrert. |

**Domener**:

* For testmiljø : `https://rrh.ppe.brreg.no`
* For produksjon: `https://rrh.brreg.no`

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer. Forespørselen valideres og returnerer opplysninger om reelle rettighetshavere.

#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.

#### Validering

* Forespørselen skal alltid inneholde organisasjonsnummeret det gjøres oppslag på.
* Dersom forespørselen inneholder et organisasjonsnummer som ikke er lovlig oppbygd, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 samt et dokument (på JSON-format) i retur. JSON-dokumentet inneholder opplysninger om reelle rettighetshavere.


#### Eksempelrespons for oppslag på organisasjonsnummer
***Eksempelresponsen er kun et utkast, og strukturen kan endre seg***

```json
{
  "registreringId": "83201f83-b92a-484c-a92c-3d5736fd1adc",
  "registreringStatus": {
    "kode": "registreringstatus.regi",
    "kodetekst": "Reelle rettighetshavere er registrert"
  },
  "registrertDato": "2022-12-15T12:00:06.231509Z",
  "reelleRettighetshavereStatus": {
    "kode": "reellerettighetshaverestatus.arid",
    "kodetekst": "Virksomheten har meldt at de har reelle rettighetshavere, og at alle reelle rettighetshavere er identifisert"
  },
  "registreringspliktigVirksomhet": {
    "organisasjonsnummer": "111111111"
  },
  "reelleRettighetshavere": [
    {
      "folkeregistrertPerson": {
        "foedselsdato": "2002-11-05",
        "foedselsaar": "2002",
        "navn": {
          "fornavn": "STOLT EFFEKTIV",
          "mellomnavn": "KUL",
          "etternavn": "PARASOLL"
        },
        "erDoed": false,
        "statsborgerskap": [
          {
            "landkode": "NOR",
            "land": "Norge"
          },
          {
            "landkode": "MEX",
            "land": "Mexico"
          }
        ]
      },
      "bostedsland": {
        "landkode": "NOR",
        "land": "Norge"
      },
      "erUnntattFraInnsyn": false,
      "posisjoner": [
        {
          "type": {
            "kode": "posisjontype.eier",
            "kodetekst": "Eierskap"
          },
          "stoerrelseIntervall": {
            "kode": "stoerrelseintervall.int2",
            "kodetekst": "50% - 74,99%"
          },
          "grunnlag": [
            {
              "kode": "grunnlagtype.dire",
              "kodetekst": "Direkte"
            }
          ]
        }
      ],
      "foerstRegistrertDato": "2022-12-16T12:00:06.242Z",
      "endretDato": "2022-12-16T12:00:06.242Z"
    },
    {
      "utenlandskPerson": {
        "foedselsdato": "1983-03-24",
        "foedselsaar": "1983",
        "fulltNavn": "GILL BATES",
        "statsborgerskap": [
          {
            "landkode": "DEU",
            "land": "Tyskland"
          },
          {
            "landkode": "SWE",
            "land": "Sverige"
          },
          {
            "landkode": "USA",
            "land": "USA"
          }
        ]
      },
      "bostedsland": {
        "landkode": "USA",
        "land": "USA"
      },
      "erUnntattFraInnsyn": false,
      "posisjoner": [
        {
          "type": {
            "kode": "posisjontype.kont",
            "kodetekst": "Kontroll over stemmerettigheter"
          },
          "stoerrelseIntervall": {
            "kode": "stoerrelseintervall.int1",
            "kodetekst": "25,01% - 49,99%"
          },
          "grunnlag": [
            {
              "kode": "grunnlagtype.indi",
              "kodetekst": "Indirekte"
            },
            {
              "kode": "grunnlagtype.enav",
              "kodetekst": "Enighet eller avtale"
            }
          ]
        },
        {
          "type": {
            "kode": "posisjontype.ruas",
            "kodetekst": "Rett til å utpeke eller avsette minst halvparten av styremedlemmene"
          },
          "grunnlag": [
            {
              "kode": "grunnlagtype.enav",
              "kodetekst": "Enighet eller avtale"
            }
          ]
        }
      ],
      "foerstRegistrertDato": "2022-12-16T12:00:06.242Z",
      "endretDato": "2022-12-16T12:00:06.242Z"
    },
    {
      "folkeregistrertPerson": {
        "foedselsdato": "1971-07-18",
        "foedselsaar": "1971",
        "navn": {
          "fornavn": "MINIMALISTISK",
          "etternavn": "HANDLELISTE"
        },
        "erDoed": false,
        "statsborgerskap": [
          {
            "landkode": "MSR",
            "land": "Montserrat"
          }
        ]
      },
      "bostedsland": {
        "landkode": "NOR",
        "land": "Norge"
      },
      "erUnntattFraInnsyn": false,
      "posisjoner": [
        {
          "type": {
            "kode": "posisjontype.anne",
            "kodetekst": "Kontroll på annen måte"
          },
          "grunnlag": [],
          "beskrivelseAnnenMaate": "Beskrivelse av hva kontrollen går ut på."
        }
      ],
      "foerstRegistrertDato": "2022-12-16T12:00:06.251Z",
      "endretDato": "2022-12-16T12:00:06.251Z"
    }
  ]
}
```

---


## HTTP-statuskoder

| HTTP-kode                 | Beskrivelse                                                                                                                                                                   |
|:------------------------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200 OK                    | Henting av data gikk bra                                                                                                                                                      |
| 400 Bad Request           | Feil i spørring. Applikasjonen vil gi en detaljert feilmelding for hva som er feil med spørring                                                                               |
| 404 Not Found             | Virksomheten har ikke registrert reelle rettighetshavere                                                                                                                      |
| 500 Internal Server Error | Intern feil i tjenesten, for eksempel at en underliggende datakilde ikke svarer                                                                                               |

## Ordliste

Definisjoner på begrep som er brukt i denne dokumentasjonen.

| Begrep              | Definisjon                                                                                                          |
|:--------------------|:--------------------------------------------------------------------------------------------------------------------|
| API                 | Programmeringsgrensesnitt                                                                                           |
| Åpent API           | Et API som ikke krever autorisering/autentisering                                                                   |
| Reell rettighet     | En reell rettighet for en gitt virksomhet inneholder en liste med reelle rettighetshavere, hvis dette er registrert |
| HTTP                | Datakommunikasjonsstandard                                                                                          |
| HTTP-statuskoder    | Statuskoder for datakommunikasjonsstandard                                                                          |
| REST                | Datakommunikasjonmønster                                                                                            |
| JSON                | Åpen standard for dataformat                                                                                        |
| Organisasjonsnummer | Identifikasjonsnummer for virksomhet                                                                                |

---
