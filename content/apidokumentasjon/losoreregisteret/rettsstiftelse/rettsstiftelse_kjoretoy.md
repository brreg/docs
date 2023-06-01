---
title: Henting av rettsstiftelser knyttet til kjøretøy
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 120
---

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                      | Beskrivelse                                                                                   |
|:------------- |:---------------------------------------------------------|:----------------------------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/v2/rettsstiftelse/regnr/\{regnr\}?language={language} | Hent opplysninger om rettsstiftelser knyttet til et registreringsnummer. Language er valgfri. |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Oppslag på registreringsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et registreringsnummer, forespørselen valideres før utførelsen og returnerer opplysninger om kun aktive rettsstiftelser på registreringsnummeret.

#### Request

Tar i mot et registreringsnummer (regnr) som del av URL.
Den valgfrie query parameteren "language" angir språkkode (ISO 639-2) for hvilket språk som skal benyttes for beskrivelser i responsen. Hvis den ikke er angitt benyttes norsk bokmål (NOB).

#### Validering

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens orgnummer, og dette orgnummeret skal være gyldig samt ha en gyldig avtale om å kunne hente ut opplysninger i Løsøreregisteret.
* Forespørselen skal alltid inneholde regnr som det gjøres oppslag på.
* Dersom forespørselen inneholder et regnr som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.
* Hvis "language" er angitt må verdien være en støttet språkkode, hvis ikke returneres det en feilmelding med informasjon om støttede språkkoder.

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "sokeparameter": "AB52874",
  "antallRettsstiftelser": 1,
  "oppslagstidspunkt": "2023-05-31T09:23:14.026651+02:00",
  "rettsstiftelse": [
    {
      "dokumentnummer": "1000125407",
      "type": "rettsstiftelsestype.pbf",
      "typeBeskrivelse": "Privat beslagsforbud",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2023-05-09T21:00:00+02:00",
      "avgrensingRettsstiftelse": "Beslagsforbudet skal gjelde til 14.05.2080. ",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.erverver",
          "rolletypeBeskrivelse": "Erverver",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "FRYKTLØS",
              "etternavn": "TURBIN"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "adressenavn": "Borgundsvegen",
              "nummer": {
                "nummer": "226"
              },
              "bruksenhetsnummer": "H0201",
              "poststed": {
                "navn": "BORGUND",
                "postnummer": "6888"
              },
              "kommune": {
                "kommunenummer": "4642",
                "kommunenavn": "Lærdal"
              }
            }
          }
        },
        {
          "rolletype": "rolletype.overdrager",
          "rolletypeBeskrivelse": "Overdrager",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "MODIG",
              "etternavn": "TRAFIKKORK"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "adressenavn": "Øvre Helle",
              "nummer": {
                "nummer": "23"
              },
              "bruksenhetsnummer": "H0101",
              "poststed": {
                "navn": "KONSMO",
                "postnummer": "4525"
              },
              "kommune": {
                "kommunenummer": "4225",
                "kommunenavn": "Lyngdal"
              }
            }
          }
        },
        {
          "rolletype": "rolletype.tillitsmann",
          "rolletypeBeskrivelse": "Tillitsmann",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.annenaktor",
            "navn": "Advokat Lars Larsen"
          }
        }
      ],
      "formuesgode": [
        {
          "identifiseringsmate": "identifiseringsmate.entydig",
          "type": "formuesgodetype.mv.e",
          "typeBeskrivelse": "Registrert motorvogn",
          "eierandel": {},
          "registreringsnummerMotorvogn": "AB52874",
          "historiskRegistreringsnummerMotorvogn": []
        },
        {
          "identifiseringsmate": "identifiseringsmate.entydig",
          "type": "formuesgodetype.mv.e",
          "typeBeskrivelse": "Registrert motorvogn",
          "eierandel": {
            "teller": 1,
            "nevner": 1
          },
          "registreringsnummerMotorvogn": "AB12345",
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
