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
  "registreringId": "1f92ac29-7b4f-4f6b-b402-6e9bc7a3ff59",
  "registreringStatus": {
    "kode": "registreringstatus.regi",
    "beskrivelse": "Reelle rettighetshavere er registrert"
  },
  "gjelderFraDato": "2022-09-06T09:17:39.87542Z",
  "reelleRettighetshavereStatus": {
    "kode": "reellerettighetshaverestatus.arid",
    "beskrivelse": "Alle reelle rettighetshavere kan identifiseres"
  },
  "reelleRettighetshavere": [
    {
      "foedselsdato": "2002-11-05",
      "foedselsaar": "2002",
      "navn": {
        "fornavn": "STOLT EFFEKTIV",
        "mellomnavn": "KUL",
        "etternavn": "PARASOLL",
        "fulltNavn": "STOLT EFFEKTIV KUL PARASOLL"
      },
      "foerstRegistrertDato": "2022-09-06T09:17:39.275205Z",
      "endretDato": "2022-09-06T09:17:39.275205Z",
      "statsborgerskap": [
        {
          "landkode": "NOR",
          "land": "Norge"
        },
        {
          "landkode": "MEX",
          "land": "Mexico"
        }
      ],
      "bostedsland": {
        "landkode": "NOR",
        "land": "Norge"
      },
      "erDoed": false,
      "erUnntattFraInnsyn": false,
      "posisjoner": [
        {
          "posisjonType": {
            "kode": "posisjontype.eier",
            "beskrivelse": "Eierskap"
          },
          "stoerrelseIntervall": {
            "kode": "stoerrelseintervall.int2",
            "beskrivelse": "50% - 74,99%"
          },
          "grunnlag": [
            {
              "grunnlagType": {
                "kode": "grunnlagtype.dire",
                "beskrivelse": "Direkte"
              }
            },
            {
              "grunnlagType": {
                "kode": "grunnlagtype.indi",
                "beskrivelse": "Indirekte"
              }
            }
          ]
        }
      ]
    },
    {
      "foedselsdato": "1983-12-01",
      "foedselsaar": "1983",
      "navn": {
        "fulltNavn": "TOM SVENSKE NELSON"
      },
      "foerstRegistrertDato": "2022-09-06T09:17:39.275205Z",
      "endretDato": "2022-09-06T09:17:39.275205Z",
      "statsborgerskap": [
        {
          "landkode": "SWE",
          "land": "Sverige"
        }
      ],
      "bostedsland": {
        "landkode": "SWE",
        "land": "Sverige"
      },
      "erDoed": false,
      "erUnntattFraInnsyn": false,
      "posisjoner": [
        {
          "posisjonType": {
            "kode": "posisjontype.eier",
            "beskrivelse": "Eierskap"
          },
          "stoerrelseIntervall": {
            "kode": "stoerrelseintervall.int1",
            "beskrivelse": "25,01% - 49,99%"
          },
          "grunnlag": [
            {
              "grunnlagType": {
                "kode": "grunnlagtype.indi",
                "beskrivelse": "Indirekte"
              }
            }
          ]
        },
        {
          "posisjonType": {
            "kode": "posisjontype.ruas",
            "beskrivelse": "Rett til å utpeke eller avsette minst halvparten av styremedlemmene"
          },
          "grunnlag": [
            {
              "grunnlagType": {
                "kode": "grunnlagtype.enav",
                "beskrivelse": "Enighet eller avtale"
              }
            }
          ]
        }
      ]
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
