---
title: Åpent API
description: Beskrivelse av Åpent API innen domene Reelle rettighetshavere
weight: 100
---


## Innledning
Det åpne API'et tilbyr oppslag på organisasjonsnummer som gir informasjon om reelle rettighetshavere.

## API-referanse

Denne tjenesten tilbyr opplysninger om fysiske personer som er reelle rettighetshavere i virksomheten, samt hvilke reelle rettigheter disse har.

[Lenke til Swagger](https://reelle-opendata-api.apps.ocp-prd.regsys.brreg.no/swagger-ui/index.html#/reelle%20rettigheter/hentReellRettighet) (Har de tilgang til Swagger?)

[Swagger-dokumentasjon](https://raw.githubusercontent.com/brreg/openAPI/master/specs/reelle-opendata-api.yaml)
(last ned [Swagger-UI](https://github.com/swagger-api/swagger-ui) og utforsk linken)


## Sikkerhetsmekanismer
Siden dette er et åpent API er det ingen sikkerhetsmekanismer.

## Skjerming

Om en reell rettighetshaver er mindreårig eller unntatt fra innsyn, vil enkelte personopplysninger være skjermet.

#### For en skjermet rettighetshaver vil responen kun inneholde:
* fødselsaar
* statsborgerskap
* bostedsland
* posisjon

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                                                    | Beskrivelse                                                                            |
|:------------- |:-------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------|
| GET           | https://\{domene\}/rrh/api/reelle-rettighetshavere/{organisasjonsnummer}                               | Hent opplysninger om reell rettighetshaver på gitt organisasjonsnummer. |

**Domener**:

* For testmiljø (ppe): `https://reelle-opendata-api.apps.ocp-ppe.regsys.brreg.no`
* For prod: `https://reelle-opendata-api.brreg.no` ?

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer. Forespørselen valideres og returnerer opplysninger om reelle rettighetshavere.

#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.

#### Validering

* Forespørselen skal alltid inneholde organisasjonsnummeret det gjøres oppslag på.
* Dersom forespørselen inneholder et organisasjonsnummer som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at organisasjonsnummeret er registrert i Enhetsregisteret. Dersom det ikke er registrert returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 samt et dokument (på JSON-format) i retur. JSON-dokumentet inneholder opplysninger om reelle rettighetshavere.

<details><summary>**Eksempelrespons**</summary><p>

##### Eksempelrespons for oppslag på organisasjonsnummer

```json
{
  "registreringId": "6f2baebd-44bc-47dc-9a1e-d9131a4219be",
  "registreringStatus": {
    "kode": "registreringstatus.regi",
    "beskrivelse": null
  },
  "gjelderFraDato": "2022-08-25T11:18:03.423645Z",
  "reelleRettighetshavereStatus": {
    "kode": "reellerettighetshaverestatus.arid",
    "beskrivelse": null
  },
  "reelleRettighetshavere": [
    {
      "foedselsdato": "1982-03-23",
      "foedselsaar": "1982",
      "navn": {
        "fornavn": null,
        "mellomnavn": null,
        "etternavn": null,
        "fulltNavn": "Dansk Danskesen"
      },
      "foerstRegistrertDato": "2022-08-19T12:28:06.674996Z",
      "endretDato": "2022-08-25T11:18:01.231688Z",
      "statsborgerskap": [
        {
          "landkode": "DK",
          "land": null
        }
      ],
      "bostedsland": {
        "landkode": "DK",
        "land": null
      },
      "erDoed": null,
      "erUnntattFraInnsyn": null,
      "posisjoner": [
        {
          "posisjonType": {
            "kode": "posisjontype.eier",
            "beskrivelse": null
          },
          "stoerrelseIntervall": {
            "kode": "stoerrelseintervall.int3",
            "beskrivelse": null
          },
          "grunnlag": [
            {
              "grunnlagType": {
                "kode": "grunnlagtype.dire",
                "beskrivelse": null
              }
            }
          ],
          "beskrivelseAnnenMaate": null
        }
      ]
    },
    {
      "foedselsdato": "1973-03-22",
      "foedselsaar": "1973",
      "navn": {
        "fornavn": null,
        "mellomnavn": null,
        "etternavn": null,
        "fulltNavn": "Svensk Svenskesen"
      },
      "foerstRegistrertDato": "2022-08-25T11:18:01.231688Z",
      "endretDato": "2022-08-25T11:18:01.231688Z",
      "statsborgerskap": [
        {
          "landkode": "NO",
          "land": null
        }
      ],
      "bostedsland": {
        "landkode": "NO",
        "land": null
      },
      "erDoed": null,
      "erUnntattFraInnsyn": null,
      "posisjoner": [
        {
          "posisjonType": {
            "kode": "posisjontype.eier",
            "beskrivelse": null
          },
          "stoerrelseIntervall": {
            "kode": "stoerrelseintervall.int2",
            "beskrivelse": null
          },
          "grunnlag": [
            {
              "grunnlagType": {
                "kode": "grunnlagtype.dire",
                "beskrivelse": null
              }
            }
          ],
          "beskrivelseAnnenMaate": null
        }
      ]
    }
  ]
}
```

---

</p></details>

## HTTP-statuskoder

| HTTP-kode                 | Beskrivelse                                                                                                                                                 |
|:------------------------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200 OK                    | Henting av data gikk bra                                                                                                                                    |
| 400 Bad Request           | Feil i spørring. Applikasjonen vil gi en detaljert feilmelding for hva som er feil med spørring                                                             |
| 404 Not Found             | Applikasjonen vil gi informasjon om at virksomheten ikke er registreringspliktig i register over reelle rettighetshavere                                    |
| 500 Internal Server Error | Intern feil i tjenesten, for eksempel at en underliggende datakilde ikke svarer                                                                             |

## Ordliste

Definisjoner på begrep som er brukt i denne dokumentasjonen.

| Begrep              | Definisjon                                                                           |
|:--------------------|:-------------------------------------------------------------------------------------|
| API                 | Programmeringsgrensesnitt                                                            |
| HTTP                | Datakommunikasjonsstandard                                                           |
| HTTP-statuskoder    | Statuskoder for datakommunikasjonsstandard                                           |
| REST                | Datakommunikasjonmønster                                                             |
| JSON                | Åpen standard for dataformat                                                         |
| Organisasjonsnummer | Identifikasjonsnummer for virksomhet                                                 |

---
