---
title: Henting av rettsstiftelser knyttet til virksomhet
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 130
---

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                                                              | Beskrivelse                                                                                                       |
|:------------- |:-----------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------|
| GET           | https://\{domene\}/api/v2/rettsstiftelse/orgnr/\{orgnr}\?language={language}&sluttbrukerOrgNr={sluttbrukerOrgNr} | Hent opplysninger om rettsstiftelser knyttet til et organisasjonsnummer. Language og sluttbrukerOrgNr er valgfri. |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer, forespørselen valideres før utførelsen og returnerer opplysninger om kun aktive rettsstiftelser på organisasjonsnummer.  
Vi gjør oppmerksom på at heftelser og andre rettsstiftelser som gjelder *Enkeltpersonforetak* (ENK) og *Andre enkeltpersoner som registreres i tilknyttet register* (PERS), vil være registrert på innehavers fødselsnummer.

#### Request

Tar i mot et organisasjonsnummer (orgnr) som del av URL.
Den valgfrie query parameteren "language" angir språkkode (ISO 639-2) for hvilket språk som skal benyttes for beskrivelser i responsen. Hvis den ikke er angitt benyttes norsk bokmål (NOB).
Valgfri query parameter "sluttbrukerOrgNr" muliggjør at konsumenten kan presisere at oppslaget gjøres på vegne av en tredjepart som har avtale med konsumenten om uthenting av data. Dette er mest aktuelt for avtaleparter som omtales som distributører. Parameteren forventes utformet som et standard organisasjonsnummer fra Enhetsregisteret.

#### Validering av forespørsler

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens orgnummer, og dette orgnummeret skal være gyldig, samt ha en gyldig avtale om å kunne hente ut opplysninger i Løsøreregisteret.
* Forespørselen skal alltid inneholde orgnr som det gjøres oppslag på.
* Dersom forespørselen inneholder et orgnr som ikke er lovlig oppbygget, returneres det en feilmelding.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.
* Hvis "language" er angitt må verdien være en støttet språkkode, hvis ikke returneres det en feilmelding med informasjon om støttede språkkoder.
* Dersom forespørselen inneholder parameter "sluttbrukerOrgNr" som ikke er lovlig oppbygd, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "sokeparameter": "810304642",
  "antallRettsstiftelser": 1,
  "oppslagstidspunkt": "2023-05-31T08:52:33.311351+02:00",
  "rettsstiftelse": [
    {
      "dokumentnummer": "1000025203",
      "type": "rettsstiftelsestype.pfr",
      "typeBeskrivelse": "Pant i fiskeredskaper",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2022-12-15T12:38:35+01:00",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.panthaver",
          "rolletypeBeskrivelse": "Panthaver",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "navn": "INNESLUTTET LYSEGRØNN TIGER AS",
            "organisasjonsnummer": "313299767",
            "adresse": {
              "adresseType": "adressetype.ustrukturertAdresse",
              "brukskategori": "forretningsadresse",
              "adresselinje1": "Brekkaveien 1I",
              "poststed": {
                "navn": "SORTLAND",
                "postnummer": "8402"
              },
              "kommune": {
                "kommunenummer": "1870",
                "kommunenavn": "SORTLAND"
              }
            }
          }
        },
        {
          "rolletype": "rolletype.pantsetter",
          "rolletypeBeskrivelse": "Pantsetter",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810304642"
          }
        }
      ],
      "formuesgode": [
        {
          "identifiseringsmate": "identifiseringsmate.tingsinnbegrep",
          "type": "formuesgodetype.fi.t",
          "typeBeskrivelse": "Fiskeredskap",
          "eierandel": {},
          "avgrensingTingsinnbegrep": "avgrensingtingsinnbegrep.hel",
          "avgrensingTingsinnbegrepBeskrivelse": "i sin helhet, slik det er til enhver tid"
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 741000,
            "valuta": "NOK"
          }
        ]
      }
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
