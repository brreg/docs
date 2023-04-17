---
title: Henting av rettstiftelser knyttet til kjøretøy
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 120
---

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                      | Beskrivelse                                                              |
|:------------- |:---------------------------------------------------------|:-------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/v2/rettsstiftelse/regnr/\{regnr\} | Hent opplysninger om rettstiftelser knyttet til et registreringsnummer.  |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Oppslag på registreringsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et registreringsnummer, forespørselen valideres før utførelsen og returnerer opplysninger om kun aktive rettstiftelser på registreringsnummeret.

#### Request

Tar i mot et registreringsnummer (regnr) som del av URL.

#### Validering

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens orgnummer, og dette orgnummeret skal være gyldig samt ha en gyldig avtale om å kunne hente ut opplysninger i Løsøreregisteret.
* Forespørselen skal alltid inneholde regnr som det gjøres oppslag på.
* Dersom forespørselen inneholder et regnr som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "sokeparameter": "CU10100",
  "oppslagstidspunkt": "2023-03-07T13:53:55.92107+01:00",
  "antallRettsstiftelser": 2,
  "rettsstiftelse": [
    {
      "dokumentnummer": "2020000003",
      "type": "rettsstiftelsestype.utp",
      "typeBeskrivelse": "Utleggspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2020-02-26T15:15:51.14512+01:00",
      "avgrensingRettsstiftelse": "JA",
      "paategning": [
        "Påtegning"
      ],
      "rolle": [
        {
          "rolletype": "rolletype.saksoker",
          "rolletypeBeskrivelse": "Saksøker",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "USTABIL",
              "mellomnavn": "FORNUFTIG",
              "etternavn": "FJERNKONTROLL"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "OSLO",
                "postnummer": "1281"
              },
              "kommune": {
                "kommunenummer": "0301",
                "kommunenavn": "Oslo"
              },
              "vegadresseID": "00001",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Helga Vaneks vei",
              "nummer": {}
            }
          }
        }
      ],
      "formuesgode": [
        {
          "identifiseringsmate": "identifiseringsmate.entydig",
          "type": "formuesgodetype.mv.e",
          "typeBeskrivelse": "Registrert motorvogn",
          "eierandel": {
            "teller": 1,
            "nevner": 1
          },
          "registreringsnummerMotorvogn": "CU10100",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [
        {
          "dokumentnummer": "2020000001",
          "rettighetshaverFremtidig": "Pantehaver"
        }
      ],
      "krav": {
        "belop": [
          {
            "belop": 2.12,
            "valuta": "NOK"
          }
        ]
      },
      "skifteutlegg": {
        "type": "skifteutleggtype.gjeld",
        "typeBeskrivelse": "Gjeld"
      },
      "vergemaal": {
        "gjelderPersonligeForhold": true,
        "gjelderOkonomiskeForhold": false,
        "varighet": "varighet.varig",
        "varighetBeskrivelse": "varig"
      },
      "gjeldsordning": {
        "type": "gjeldsordningstype.tvungen",
        "typeBeskrivelse": "tvungen gjeldsordning",
        "periode": {
          "fraDato": "2020-04-02",
          "tilDato": "2020-08-17"
        },
        "gjeldsordningsperiodeAntallMaaneder": 10,
        "gjeldsordningsperiodeAntallAar": 2
      }
    },
    {
      "dokumentnummer": "2020000031",
      "type": "rettsstiftelsestype.utp",
      "typeBeskrivelse": "Utleggspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2020-02-26T15:15:51.14512+01:00",
      "avgrensingRettsstiftelse": "JA",
      "paategning": [
        "Påtegning"
      ],
      "rolle": [
        {
          "rolletype": "rolletype.saksoker",
          "rolletypeBeskrivelse": "Saksøker",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "USTABIL",
              "mellomnavn": "FORNUFTIG",
              "etternavn": "FJERNKONTROLL"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "OSLO",
                "postnummer": "1281"
              },
              "kommune": {
                "kommunenummer": "0301",
                "kommunenavn": "Oslo"
              },
              "vegadresseID": "00001",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Helga Vaneks vei",
              "nummer": {}
            }
          }
        }
      ],
      "formuesgode": [
        {
          "identifiseringsmate": "identifiseringsmate.entydig",
          "type": "formuesgodetype.mv.e",
          "typeBeskrivelse": "Registrert motorvogn",
          "eierandel": {
            "teller": 1,
            "nevner": 1
          },
          "registreringsnummerMotorvogn": "CU10100",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [
        {
          "dokumentnummer": "2020000001",
          "rettighetshaverFremtidig": "Pantehaver"
        }
      ],
      "krav": {
        "belop": [
          {
            "belop": 2.12,
            "valuta": "NOK"
          }
        ]
      },
      "skifteutlegg": {
        "type": "skifteutleggtype.gjeld",
        "typeBeskrivelse": "Gjeld"
      },
      "vergemaal": {
        "gjelderPersonligeForhold": true,
        "gjelderOkonomiskeForhold": false,
        "varighet": "varighet.varig",
        "varighetBeskrivelse": "varig"
      },
      "gjeldsordning": {
        "type": "gjeldsordningstype.tvungen",
        "typeBeskrivelse": "tvungen gjeldsordning",
        "periode": {
          "fraDato": "2020-04-02",
          "tilDato": "2020-08-17"
        },
        "gjeldsordningsperiodeAntallMaaneder": 10,
        "gjeldsordningsperiodeAntallAar": 2
      }
    }
  ]
}
```

---

## Feilmeldinger

Dersom man ikke får HTTP-status 200, så får man en melding fra tjenesten i JSON-format. Hvis det er ingen treff får man fortsatt 200-status.

| HTTP-kode   | Feilmelding                                                                                 |
|:----------- |:------------------------------------------------------------------------------------------- |
| 400         | Ugyldig regnr                                                                               |
| 403         | Forespørsel inneholder ingen gyldig bearer token                                            |

##### Eksempelrespons feilmelding

```json
{
  "korrelasjonsid": "cba2c68f-2f04-4104-9dbf-8e69c5e36c5c",
  "tidspunkt": "2023-03-07T13:23:35.14512+01:00",
  "feilmelding": "Feil i registreringsnummer, vennligst prøv på nytt"
}
```

---
