---
title: Henting av rettsstiftelser knyttet til person
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 140
---

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                                                          | Beskrivelse                                                                                                                |
|:------------- |:-------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/v2/rettsstiftelse/fnr/\{fnr}\?language={language}&sluttbrukerOrgNr={sluttbrukerOrgNr} | Hent opplysninger om rettsstiftelser knyttet til et fødselsnummer eller d-nummer. Language og sluttbrukerOrgNr er valgfri. |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Oppslag på fødselsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et fødselsnummer eller d-nummer, forespørselen valideres før utførelsen og returnerer opplysninger om kun aktive rettsstiftelser på fødselsnummeret eller d-nummeret.

#### Request

Tar i mot et fødselsnummer eller d-nummer (fnr) som del av URL.
Den valgfrie query parameteren "language" angir språkkode (ISO 639-2) for hvilket språk som skal benyttes for beskrivelser i responsen. Hvis den ikke er angitt benyttes norsk bokmål (NOB).
Valgfri query parameter "sluttbrukerOrgNr" muliggjør at konsumenten kan presisere at oppslaget gjøres på vegne av en tredjepart som har avtale med konsumenten om uthenting av data. Dette er mest aktuelt for avtaleparter som omtales som distributører. Parameteren forventes utformet som et standard organisasjonsnummer fra Enhetsregisteret.

#### Validering

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens orgnummer, og dette orgnummeret skal være gyldig samt ha en gyldig avtale om å kunne hente ut opplysninger i Løsøreregisteret.
* Forespørselen skal alltid inneholde fnr som det gjøres oppslag på.
* Dersom forespørselen inneholder et fnr som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.
* Hvis "language" er angitt må verdien være en støttet språkkode, hvis ikke returneres det en feilmelding med informasjon om støttede språkkoder.
* Dersom forespørselen inneholder parameter "sluttbrukerOrgNr" som ikke er lovlig oppbygd, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "sokeparameter": "11913049987",
  "antallRettsstiftelser": 1,
  "oppslagstidspunkt": "2023-05-31T09:35:51.548089+02:00",
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
          "identifiseringsmate": "identifiseringsmate.sarskilt",
          "type": "formuesgodetype.pe.s",
          "typeBeskrivelse": "Penger",
          "eierandel": {
            "teller": 1,
            "nevner": 1
          },
          "identifikator": "INGEN_BESKRIVELSE",
          "identifiseringstype": "identifiseringstype.ingenBeskrivelse",
          "identifiseringstypeBeskrivelse": "Ingen beskrivelse av formuesgode"
        }
      ],
      "prioritetsvikelse": [],
      "gjeldsomfang": "gjeldsomfang.eksisterende",
      "gjeldsomfangBeskrivelse": "Eksisterende gjeld",
      "tidsbegrensningHeftelse": "2026-03-27"
    }
  ]
}
```

---

## Feilmeldinger

Dersom man ikke får HTTP-status 200, så får man en melding fra tjenesten i JSON-format. Hvis det er ingen treff får man fortsatt 200-status.

| HTTP-kode | Feilmelding                                                      |
|:----------|:-----------------------------------------------------------------|
| 400       | Feil i fødselsnummer/organisasjonsnummer, vennligst prøv på nytt |
| 403       | Feil under autentisering av abonnent                             |

##### Eksempelrespons feilmelding

```json
{
  "korrelasjonsid": "5d217325-fa5a-47a1-8069-781fa5e1dedc",
  "tidspunkt": "2023-04-17T08:53:21.859622+02:00",
  "feilmelding": "Feil i fødselsnummer/organisasjonsnummer, vennligst prøv på nytt"
}
```

---
