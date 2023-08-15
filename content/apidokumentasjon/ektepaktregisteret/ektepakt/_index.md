---
title: Ektepakt knyttet til person
description: Beskrivelser av API innen domene Ektepaktregisteret
weight: 100
---

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                                               | Beskrivelse                                                                                         |
|:------------- |:--------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/v1/fnr/\{fnr}\?spraakkode={spraakkode} | Hent opplysninger om ektepakter knyttet til et fødselsnummer eller d-nummer. Spraakkode er valgfri. |

**Domener**:

* For testmiljø (ppe) `https://ektepaktregisteret.ppe.brreg.no/ektepakt`
* For produksjon `https://ektepaktregisteret.brreg.no/ektepakt`

### Oppslag på fødselsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et fødselsnummer eller d-nummer, forespørselen valideres før utførelsen og returnerer opplysninger om kun aktive ektepakter på fødselsnummeret eller d-nummeret.

#### Request

Tar i mot et fødselsnummer eller d-nummer (fnr) som del av URL.
Den valgfrie query parameteren "spraakkode" angir språkkode (ISO 639-2) for hvilket språk som skal benyttes for beskrivelser i responsen. Hvis den ikke er angitt benyttes norsk bokmål (NOB).

#### Validering

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens orgnummer, og dette orgnummeret skal være gyldig samt ha en gyldig avtale om å kunne hente ut opplysninger i Ektepaktregisteret.
* Forespørselen skal alltid inneholde fnr som det gjøres oppslag på.
* Dersom forespørselen inneholder et fnr som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.
* Hvis "spraakkode" er angitt må verdien være en støttet språkkode, hvis ikke returneres det en feilmelding med informasjon om støttede språkkoder.

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om ektepakten(e).

##### Eksempelrespons

```json
{
  "rolleinnehaver": "06821349425",
  "antallEktepakt": 1,
  "oppslagstidspunkt": "2023-08-11T13:29:26.101673632Z",
  "spraak": "NOB",
  "ektepakt": [
    {
      "ektepaktnummer": 1,
      "innkomsttidspunkt": "2023-06-01T03:30:00Z",
      "ektepakttype": "ektepakttype.ektepakt",
      "ektepakttypebeskrivelse": "Ektepakt",
      "status": "ektepaktstatus.tinglyst",
      "statusbeskrivelse": "Tinglyst",
      "opprettelse": "opprettelsestype.foersteOpprettelse",
      "opprettelsestypebeskrivelse": "Første gangs opprettelse av ektepakt",
      "harSupplerendeOpplysningerIDokument": false,
      "paategning": [],
      "avtaleinnhold": [
        {
          "avtaletype": "avtaletype.gave",
          "avtaletypebeskrivelse": "Ektepakten inneholder gave"
        }
      ],
      "rolle": [
        {
          "rolletype": "rolletype.ektefelle",
          "rolletypebeskrivelse": "Ektefelle",
          "person": {
            "navn": {
              "fornavn": "AUTORISERT",
              "mellomnavn": null,
              "etternavn": "INNHEGNING"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "coNavn": null,
              "adressenavnTillegg": null,
              "adressenavn": "Gaukvegen",
              "kortAdressenavn": null,
              "nummer": {
                "nummer": "13",
                "bokstav": null
              },
              "bruksenhetsnummer": "H0101",
              "vegadresseID": null,
              "poststed": {
                "navn": "KONGSVINGER",
                "postnummer": "2209"
              },
              "kommune": {
                "kommunenummer": "3401",
                "kommunenavn": "Kongsvinger"
              }
            }
          },
          "avtaleinnhold": [
            {
              "avtaletype": "avtaletype.fulltSaereie",
              "avtaletypebeskrivelse": "Vi skal ha fullt særeie"
            }
          ]
        },
        {
          "rolletype": "rolletype.ektefelle",
          "rolletypebeskrivelse": "Ektefelle",
          "person": {
            "navn": {
              "fornavn": "SORGLØS",
              "mellomnavn": null,
              "etternavn": "BOLLE"
            },
            "adresse": {
              "adresseType": "adressetype.vegadresse",
              "brukskategori": "bostedsadresse",
              "coNavn": null,
              "adressenavnTillegg": null,
              "adressenavn": "Kløvåsen",
              "kortAdressenavn": null,
              "nummer": {
                "nummer": null,
                "bokstav": null
              },
              "bruksenhetsnummer": "H0101",
              "vegadresseID": null,
              "poststed": {
                "navn": "RAMNES",
                "postnummer": "3175"
              },
              "kommune": {
                "kommunenummer": "3803",
                "kommunenavn": "Tønsberg"
              }
            }
          },
          "avtaleinnhold": [
            {
              "avtaletype": "avtaletype.delvisSaereie",
              "avtaletypebeskrivelse": "Vi skal ha delvis særeie"
            }
          ]
        }
      ]
    }
  ]
}
```

---

## Feilmeldinger

Dersom man ikke får HTTP-status 200, så får man en melding fra tjenesten i JSON-format. Hvis det er ingen treff får man fortsatt 200-status.

| HTTP-kode | Feilmelding                                  |
|:----------|:---------------------------------------------|
| 400       | Feil i fødselsnummer, vennligst prøv på nytt |
| 403       | Feil under autentisering av abonnent         |
| 500       | Tjenesten feilet på serversiden              |

##### Eksempelrespons feilmelding

```json
{
  "sokeparameter": null,
  "korrelasjonsid": "41c0b5b3-ed0a-4392-a57a-9bfc57dcd48c",
  "tidspunkt": "2023-08-11T14:27:33.724162177+02:00",
  "feilmelding": "Feil i fødselsnummer, vennligst prøv på nytt"
}
```

---
