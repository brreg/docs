---
title: Henting av rettsstiftelser knyttet til virksomhet
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 130
---

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                                          | Beskrivelse                                                              |
|:------------- |:---------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/v2/rettsstiftelse/orgnr/\{orgnr}\?sluttbrukerOrgNr={sluttbrukerOrgNr} | Hent opplysninger om rettstiftelser knyttet til et organisasjonsnummer. SluttbrukerOrgNr er valgfri  |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer, forespørselen valideres før utførelsen og returnerer opplysninger om kun aktive rettstiftelser på organisasjonsnummer.

#### Request

Tar i mot et organisasjonsnummer (orgnr) som del av URL.
Valgfri parameter "sluttbrukerOrgNr" muliggjør at konsumenten kan presisere at oppslaget gjøres på vegne av en tredjepart som har avtale med konsumenten om uthenting av data. Dette er mest aktuelt for avtaleparter som omtales som distributører. Parameteren forventes utformet som et standard organisasjonsnummer fra Enhetsregisteret.

#### Validering av forespørsler

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens orgnummer, og dette orgnummeret skal være gyldig samt ha en gyldig avtale om å kunne hente ut opplysninger i Løsøreregisteret.
* Forespørselen skal alltid inneholde orgnr som det gjøres oppslag på.
* Dersom forespørselen inneholder et orgnr som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.
* Dersom forespørselen inneholder parameter "sluttbrukerOrgNr" som ikke er lovlig oppbygd, returneres det en feilmelding

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "sokeparameter": "811087432",
  "oppslagstidspunkt": "2023-04-07T08:51:01.622294+02:00",
  "antallRettsstiftelser": 4,
  "rettsstiftelse": [
    {
      "dokumentnummer": "1000001353",
      "type": "rettsstiftelsestype.lea",
      "typeBeskrivelse": "Leasing",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2022-08-23T19:00:00.14512+02:00",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.eier",
          "rolletypeBeskrivelse": "Eier",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "ERFAREN",
              "etternavn": "COSINUS"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "KRISTIANSAND S",
                "postnummer": "4632"
              },
              "kommune": {
                "kommunenummer": "4204",
                "kommunenavn": "Kristiansand"
              },
              "vegadresseID": "14770",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Kuholmsveien",
              "nummer": {
                "nummer": "112"
              }
            }
          }
        },
        {
          "rolletype": "rolletype.leietaker",
          "rolletypeBeskrivelse": "Leietaker",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811087432"
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
          "registreringsnummerMotorvogn": "XY1012",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": []
    },
    {
      "dokumentnummer": "1000001451",
      "type": "rettsstiftelsestype.lea",
      "typeBeskrivelse": "Leasing",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2022-08-22T19:00:00.14512+02:00",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.eier",
          "rolletypeBeskrivelse": "Eier",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811087572"
          }
        },
        {
          "rolletype": "rolletype.leietaker",
          "rolletypeBeskrivelse": "Leietaker",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811087432"
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
          "registreringsnummerMotorvogn": "RE12345",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": []
    },
    {
      "dokumentnummer": "1000001516",
      "type": "rettsstiftelsestype.lea",
      "typeBeskrivelse": "Leasing",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2022-09-12T19:00:00.14512+02:00",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.eier",
          "rolletypeBeskrivelse": "Eier",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811088242"
          }
        },
        {
          "rolletype": "rolletype.leietaker",
          "rolletypeBeskrivelse": "Leietaker",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811087432"
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
          "registreringsnummerMotorvogn": "RE12345",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": []
    },
    {
      "dokumentnummer": "1000001565",
      "type": "rettsstiftelsestype.lea",
      "typeBeskrivelse": "Leasing",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2022-09-12T19:00:00.14512+02:00",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.eier",
          "rolletypeBeskrivelse": "Eier",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811087572"
          }
        },
        {
          "rolletype": "rolletype.leietaker",
          "rolletypeBeskrivelse": "Leietaker",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811087432"
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
          "registreringsnummerMotorvogn": "RE12345",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": []
    }
  ]
}
```

---

## Feilmeldinger

Dersom man ikke får HTTP-status 200, så får man en melding fra tjenesten i JSON-format. Hvis det er ingen treff, får man fortsatt 200-status.

| HTTP-kode   | Feilmelding                                                                       |
|:----------- |:----------------------------------------------------------------------------------|
| 400         | Feil i fødselsnummer/organisasjonsnummer, vennligst prøv på nytt                  |
| 403         | Feil under autentisering av abonnent                                              |

##### Eksempelrespons feilmelding

```json
{
  "korrelasjonsid": "c1c188f5-2fe2-4a1b-97f1-360fff37ea21",
  "tidspunkt": "2023-04-17T08:52:52.960824+02:00",
  "feilmelding": "Feil i fødselsnummer/organisasjonsnummer, vennligst prøv på nytt"
}
```

---
