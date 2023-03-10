---
title: Henting av rettsstiftelser knyttet til person
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 140
---

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                                      | Beskrivelse                                                                      |
|:------------- |:-----------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/v2/rettsstiftelse/fnr/\{fnr}\?sluttbrukerOrgNr={sluttbrukerOrgNr} | Hent opplysninger om rettstiftelser knyttet til et fødselsnummer eller d-nummer. SluttbrukerOrgNr er valgfri |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Oppslag på fødselsnummer

#### Beskrajourivelse

Tjenesten tar imot en forespørsel om oppslag på et fødselsnummer eller d-nummer, forespørselen valideres før utførelsen og returnerer opplysninger om kun aktive rettstiftelser på fødselsnummeret eller d-nummeret.

#### Request

Tar i mot et fødselsnummer eller d-nummer (fnr) som del av URL.
Valgfri parameter "sluttbrukerOrgNr" muliggjør at konsumenten kan presisere at oppslaget gjøres på vegne av en tredjepart som har avtale med konsumenten om uthenting av data. Dette er mest aktuelt for avtaleparter som omtales som distributører. Parameteren forventes utformet som et standard organisasjonsnummer fra Enhetsregisteret.

#### Validering

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens orgnummer, og dette orgnummeret skal være gyldig samt ha en gyldig avtale om å kunne hente ut opplysninger i Løsøreregisteret.
* Forespørselen skal alltid inneholde fnr som det gjøres oppslag på.
* Dersom forespørselen inneholder et fnr som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.
* Dersom forespørselen inneholder parameter "sluttbrukerOrgNr" som ikke er lovlig oppbygd, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "sokeparameter": "28884199370",
  "oppslagstidspunkt": "2023-03-07T14:22:34.823226",
  "antallRettsstiftelser": 8,
  "rettsstiftelse": [
    {
      "dokumentnummer": "1000027103",
      "type": "rettsstiftelsestype.utp",
      "typeBeskrivelse": "Utleggspant",
      "status": "statusregistreringsobjekt.nt",
      "statusBeskrivelse": "nektet tinglyst",
      "innkomsttidspunkt": "2023-02-16T20:00:00Z",
      "beslutningstidspunkt": "2023-02-20T07:00:00Z",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.namsmyndighet",
          "rolletypeBeskrivelse": "Namsmyndighet",
          "rollegruppetype": "rollegruppe.oppr",
          "rollegruppetypeBeskrivelse": "Oppretter",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810004312"
          }
        },
        {
          "rolletype": "rolletype.prosessfullmektig",
          "rolletypeBeskrivelse": "Prosessfullmektig",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810004312"
          }
        },
        {
          "rolletype": "rolletype.saksoker",
          "rolletypeBeskrivelse": "Saksøker",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810004142"
          }
        },
        {
          "rolletype": "rolletype.saksokt",
          "rolletypeBeskrivelse": "Saksøkt",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SVIMMEL",
              "etternavn": "BEVILLING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "SKJOLD",
                "postnummer": "5574"
              },
              "kommune": {
                "kommunenummer": "1160",
                "kommunenavn": "Vindafjord"
              },
              "vegadresseID": "1021",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Haraldseidvågen",
              "nummer": {
                "nummer": "264"
              }
            }
          }
        }
      ],
      "formuesgode": [
        {
          "identifiseringsmate": "identifiseringsmate.sarskilt",
          "type": "formuesgodetype.pe.s",
          "typeBeskrivelse": "Penger",
          "eierandel": {
            "teller": 1,
            "nevner": 1
          },
          "identifikator": "Innestående på konto",
          "identifiseringstype": "identifiseringstype.konto",
          "identifiseringstypeBeskrivelse": "Innestående på konto"
        },
        {
          "identifiseringsmate": "identifiseringsmate.entydig",
          "type": "formuesgodetype.mv.e",
          "typeBeskrivelse": "Registrert motorvogn",
          "eierandel": {
            "teller": 1,
            "nevner": 1
          },
          "registreringsnummerMotorvogn": "KK8844",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 18644.00,
            "valuta": "NOK"
          }
        ]
      }
    },
    {
      "dokumentnummer": "1000026992",
      "type": "rettsstiftelsestype.sap",
      "typeBeskrivelse": "Salgspant",
      "status": "statusregistreringsobjekt.nt",
      "statusBeskrivelse": "nektet tinglyst",
      "innkomsttidspunkt": "2023-02-12T20:00:00Z",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.panthaver",
          "rolletypeBeskrivelse": "Panthaver",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810004312"
          }
        },
        {
          "rolletype": "rolletype.pantsetter",
          "rolletypeBeskrivelse": "Pantsetter",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SVIMMEL",
              "etternavn": "BEVILLING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "SKJOLD",
                "postnummer": "5574"
              },
              "kommune": {
                "kommunenummer": "1160",
                "kommunenavn": "Vindafjord"
              },
              "vegadresseID": "1021",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Haraldseidvågen",
              "nummer": {
                "nummer": "264"
              }
            }
          }
        }
      ],
      "formuesgode": [],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 320000.00,
            "valuta": "NOK"
          }
        ],
        "kravSalgspant": "kravsalgspant.lan.til.kjoper",
        "kravSalgspantBeskrivelse": "lån som tredjeperson har ydet kjøperen"
      }
    },
    {
      "dokumentnummer": "1000026644",
      "type": "rettsstiftelsestype.utp",
      "typeBeskrivelse": "Utleggspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2023-02-02T20:00:00Z",
      "beslutningstidspunkt": "2023-01-30T23:00:00Z",
      "paategning": [
        "Dokumentet har ved en feil vært ute av registeret."
      ],
      "rolle": [
        {
          "rolletype": "rolletype.namsmyndighet",
          "rolletypeBeskrivelse": "Namsmyndighet",
          "rollegruppetype": "rollegruppe.oppr",
          "rollegruppetypeBeskrivelse": "Oppretter",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811086002"
          }
        },
        {
          "rolletype": "rolletype.prosessfullmektig",
          "rolletypeBeskrivelse": "Prosessfullmektig",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810715782"
          }
        },
        {
          "rolletype": "rolletype.saksoker",
          "rolletypeBeskrivelse": "Saksøker",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810004312"
          }
        },
        {
          "rolletype": "rolletype.saksokt",
          "rolletypeBeskrivelse": "Saksøkt",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SVIMMEL",
              "etternavn": "BEVILLING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "SKJOLD",
                "postnummer": "5574"
              },
              "kommune": {
                "kommunenummer": "1160",
                "kommunenavn": "Vindafjord"
              },
              "vegadresseID": "1021",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Haraldseidvågen",
              "nummer": {
                "nummer": "264"
              }
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
          "registreringsnummerMotorvogn": "FT65432",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 13200.00,
            "valuta": "NOK"
          }
        ]
      }
    },
    {
      "dokumentnummer": "1000026966",
      "type": "rettsstiftelsestype.sap",
      "typeBeskrivelse": "Salgspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2023-02-12T20:00:00Z",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.panthaver",
          "rolletypeBeskrivelse": "Panthaver",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810601302"
          }
        },
        {
          "rolletype": "rolletype.pantsetter",
          "rolletypeBeskrivelse": "Pantsetter",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SVIMMEL",
              "etternavn": "BEVILLING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "SKJOLD",
                "postnummer": "5574"
              },
              "kommune": {
                "kommunenummer": "1160",
                "kommunenavn": "Vindafjord"
              },
              "vegadresseID": "1021",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Haraldseidvågen",
              "nummer": {
                "nummer": "264"
              }
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
          "registreringsnummerMotorvogn": "CV11114",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 15963.00,
            "valuta": "EUR"
          },
          {
            "belop": 369800.00,
            "valuta": "NOK"
          }
        ],
        "kravSalgspant": "kravsalgspant.lan.til.kjoper",
        "kravSalgspantBeskrivelse": "lån som tredjeperson har ydet kjøperen"
      }
    },
    {
      "dokumentnummer": "1000026967",
      "type": "rettsstiftelsestype.sap",
      "typeBeskrivelse": "Salgspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2023-02-12T20:00:00Z",
      "paategning": [
        "Dokumentet har ved en feil vært ute av registeret."
      ],
      "rolle": [
        {
          "rolletype": "rolletype.panthaver",
          "rolletypeBeskrivelse": "Panthaver",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810599332"
          }
        },
        {
          "rolletype": "rolletype.pantsetter",
          "rolletypeBeskrivelse": "Pantsetter",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SVIMMEL",
              "etternavn": "BEVILLING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "SKJOLD",
                "postnummer": "5574"
              },
              "kommune": {
                "kommunenummer": "1160",
                "kommunenavn": "Vindafjord"
              },
              "vegadresseID": "1021",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Haraldseidvågen",
              "nummer": {
                "nummer": "264"
              }
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
          "registreringsnummerMotorvogn": "CV11116",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 249600.00,
            "valuta": "NOK"
          },
          {
            "belop": 24900.00,
            "valuta": "EUR"
          }
        ],
        "kravSalgspant": "kravsalgspant.lan.til.kjoper",
        "kravSalgspantBeskrivelse": "lån som tredjeperson har ydet kjøperen"
      }
    },
    {
      "dokumentnummer": "1000027142",
      "type": "rettsstiftelsestype.utp",
      "typeBeskrivelse": "Utleggspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2023-02-16T20:00:00Z",
      "beslutningstidspunkt": "2023-01-30T06:40:00Z",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.saksoker",
          "rolletypeBeskrivelse": "Saksøker",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810602082"
          }
        },
        {
          "rolletype": "rolletype.saksokt",
          "rolletypeBeskrivelse": "Saksøkt",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SVIMMEL",
              "etternavn": "BEVILLING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "SKJOLD",
                "postnummer": "5574"
              },
              "kommune": {
                "kommunenummer": "1160",
                "kommunenavn": "Vindafjord"
              },
              "vegadresseID": "1021",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Haraldseidvågen",
              "nummer": {
                "nummer": "264"
              }
            }
          }
        },
        {
          "rolletype": "rolletype.namsmyndighet",
          "rolletypeBeskrivelse": "Namsmyndighet",
          "rollegruppetype": "rollegruppe.oppr",
          "rollegruppetypeBeskrivelse": "Oppretter",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810004312"
          }
        },
        {
          "rolletype": "rolletype.prosessfullmektig",
          "rolletypeBeskrivelse": "Prosessfullmektig",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810003502"
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
          "registreringsnummerMotorvogn": "TF99999",
          "historiskRegistreringsnummerMotorvogn": []
        },
        {
          "identifiseringsmate": "identifiseringsmate.sarskilt",
          "type": "formuesgodetype.af.s",
          "typeBeskrivelse": "Annet formuesgode",
          "eierandel": {
            "teller": 1,
            "nevner": 1
          },
          "identifikator": "10 Aksjer i 810003642, Beltegraver Hitachi 2021 mod serienr 12345868, Ford Taurus",
          "identifiseringstype": "identifiseringstype.generellBeskrivelse",
          "identifiseringstypeBeskrivelse": "Beskrivelse av formuesgode"
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 365123.00,
            "valuta": "NOK"
          }
        ]
      }
    },
    {
      "dokumentnummer": "1000027169",
      "type": "rettsstiftelsestype.utp",
      "typeBeskrivelse": "Utleggspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2023-02-16T20:00:00Z",
      "beslutningstidspunkt": "2022-01-02T06:00:00Z",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.namsmyndighet",
          "rolletypeBeskrivelse": "Namsmyndighet",
          "rollegruppetype": "rollegruppe.oppr",
          "rollegruppetypeBeskrivelse": "Oppretter",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810003812"
          }
        },
        {
          "rolletype": "rolletype.prosessfullmektig",
          "rolletypeBeskrivelse": "Prosessfullmektig",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810601302"
          }
        },
        {
          "rolletype": "rolletype.saksoker",
          "rolletypeBeskrivelse": "Saksøker",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "NONFIGURATIV",
              "etternavn": "MEDISTERDEIG"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "ASKIM",
                "postnummer": "1832"
              },
              "kommune": {
                "kommunenummer": "3014",
                "kommunenavn": "Indre Østfold"
              },
              "vegadresseID": "24450",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Kalfaret",
              "nummer": {
                "nummer": "4",
                "bokstav": "A"
              }
            }
          }
        },
        {
          "rolletype": "rolletype.saksokt",
          "rolletypeBeskrivelse": "Saksøkt",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SVIMMEL",
              "etternavn": "BEVILLING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "SKJOLD",
                "postnummer": "5574"
              },
              "kommune": {
                "kommunenummer": "1160",
                "kommunenavn": "Vindafjord"
              },
              "vegadresseID": "1021",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Haraldseidvågen",
              "nummer": {
                "nummer": "264"
              }
            }
          }
        }
      ],
      "formuesgode": [
        {
          "identifiseringsmate": "identifiseringsmate.sarskilt",
          "type": "formuesgodetype.sb.s",
          "typeBeskrivelse": "Småbåt",
          "eierandel": {
            "teller": 1,
            "nevner": 1
          },
          "identifikator": "Askeladden 14 fot",
          "identifiseringstype": "identifiseringstype.generellBeskrivelse",
          "identifiseringstypeBeskrivelse": "Beskrivelse av formuesgode"
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 54215.00,
            "valuta": "NOK"
          }
        ]
      }
    },
    {
      "dokumentnummer": "1000027441",
      "type": "rettsstiftelsestype.bff",
      "typeBeskrivelse": "Beslutning om forvaltning av formue",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2023-03-01T20:00:00Z",
      "beslutningstidspunkt": "2023-02-27T23:00:00Z",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.domstol",
          "rolletypeBeskrivelse": "Domstol",
          "rollegruppetype": "rollegruppe.oppr",
          "rollegruppetypeBeskrivelse": "Oppretter",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810003812"
          }
        },
        {
          "rolletype": "rolletype.person",
          "rolletypeBeskrivelse": "Person",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SVIMMEL",
              "etternavn": "BEVILLING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "poststed": {
                "navn": "SKJOLD",
                "postnummer": "5574"
              },
              "kommune": {
                "kommunenummer": "1160",
                "kommunenavn": "Vindafjord"
              },
              "vegadresseID": "1021",
              "bruksenhetsnummer": "H0101",
              "adressenavn": "Haraldseidvågen",
              "nummer": {
                "nummer": "264"
              }
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
          "registreringsnummerMotorvogn": "CU10011",
          "historiskRegistreringsnummerMotorvogn": []
        },
        {
          "identifiseringsmate": "identifiseringsmate.entydig",
          "type": "formuesgodetype.mv.e",
          "typeBeskrivelse": "Registrert motorvogn",
          "eierandel": {},
          "registreringsnummerMotorvogn": "XV12345",
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

Dersom man ikke får HTTP-status 200, så får man en melding fra tjenesten i JSON-format.

| HTTP-kode | Feilmelding                                                      |
|:----------|:-----------------------------------------------------------------|
| 400       | Feil i fødselsnummer/organisasjonsnummer, vennligst prøv på nytt |
| 403       | Feil under autentisering av abonnent                             |
| 404       | fnr mangler                                                      |

##### Eksempelrespons feilmelding

```json
{
  "korrelasjonsid": "5d217325-fa5a-47a1-8069-781fa5e1dedc",
  "tidspunkt": "2023-03-07 13:21:45",
  "feilmelding": "Feil i fødselsnummer/organisasjonsnummer, vennligst prøv på nytt"
}
```

---
