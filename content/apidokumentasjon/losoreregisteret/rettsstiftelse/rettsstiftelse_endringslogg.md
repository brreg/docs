---
title: Endringslogg
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 160
---

## Bruksmønster

Se [siden for totalbestand]({{<ref "rettsstiftelse_totalbestand.md">}}) for en helhetlig oversikt av bruksmønsteret for endringslogg og totalbestand.

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                   | Beskrivelse                                                                   |
|:------------- |:------------------------------------------------------|:------------------------------------------------------------------------------|
| POST          | https://\{domene\}/api/v2/rettsstiftelse/endringslogg | Hent opplysninger endringer på rettstiftelser fra et ønsket tidspunkt         |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Henting av endringslogg

#### Beskrivelse

Endepunktet tar imot en forespørsel med felter *lowerCutoff* for tidspunkt-avgrensning og *lastSortValues* for paginering.

*Merk:* Kun rettsstiftelser nyere enn 30 dager vil inkluderes i responsen, uavhengig av om *lowerCutoff* settes før dette.

#### Validering

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens organisasjonsnummer, og dette organisasjonsnummeret skal være gyldig samt ha en gyldig avtale for å kunne hente ut opplysninger i Løsøreregisteret.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.

## Paginering

Grunnet store datamengder er det nødvendig å paginere requests og respons til tjenesten. Dette gjøres ved hjelp av feltet *"lastSortValues"*.
For å få første page skal dette feltet være *null*, deretter skal man sette dette feltet til verdien av feltet *"sortValues"* fra forrige response.
Dette gjør at tjenesten er istand til å vite hvilken side av datasettet den skal returnere.

*Merk:* Siste side vil ha 0 rettsstiftelser, og vil ikke inneholde *"sortValues"*.
Dette vil gjelde første side hvis det ikke har vært endringer på rettsstiftelser etter tidspunktet angitt av *lowerCutoff*.

#### Request
Første request før paginering vil kunne se slik ut:
```json
{
  "lowerCutoff": "2023-03-01T00:00:00.000+02:00",
  "lastSortValues": null
}
```
Deretter vil man, basert på *"sortValues"* fra forrige [response](#eksempelrespons), utforme en request som dette:
```json
{
  "lowerCutoff": "2023-03-01T00:00:00.000+02:00",
  "lastSortValues": [
    "1678199182817",
    "24053b47-41bb-4f6b-b3ad-306fade98352"
  ]
}
```

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "sistEndretSisteInnslag": "2023-03-07T14:26:22.817126+01:00",
  "sortValues": [
    "1678199182817",
    "24053b47-41bb-4f6b-b3ad-306fade98352"
  ],
  "antallRettsstiftelser": 2,
  "rettsstiftelse": [
    {
      "dokumentnummer": "1000001790",
      "type": "rettsstiftelsestype.frh",
      "typeBeskrivelse": "Fratakelse av rettslig handleevne",
      "status": "statusregistreringsobjekt.sl",
      "statusBeskrivelse": "slettet",
      "innkomsttidspunkt": "2021-01-10T16:49:58.023+01:00",
      "beslutningstidspunkt": "2021-01-10T10:02:00+01:00",
      "utlopRettsvernstid": "2023-03-04",
      "slettet": "2023-03-06",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.domstol",
          "rolletypeBeskrivelse": "Domstol",
          "rollegruppetype": "rollegruppe.oppr",
          "rollegruppetypeBeskrivelse": "Oppretter",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811069302"
          }
        },
        {
          "rolletype": "rolletype.undervergemal",
          "rolletypeBeskrivelse": "Under vergemål",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "SJENERT",
              "etternavn": "INDREFILET"
            },
            "fodselsnummerEllerDNummer": "12810449614"
          }
        },
        {
          "rolletype": "rolletype.verge",
          "rolletypeBeskrivelse": "Verge",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "USYMMETRISK",
              "mellomnavn": "SOLSIKKE",
              "etternavn": "ABAKUS"
            },
            "fodselsnummerEllerDNummer": "14865095369"
          }
        }
      ],
      "formuesgode": [],
      "prioritetsvikelse": [],
      "vergemaal": {
        "gjelderPersonligeForhold": true,
        "gjelderOkonomiskeForhold": false,
        "varighet": "varighet.varig",
        "varighetBeskrivelse": "varig",
        "tidsbegrensetTilDato": "2023-03-04"
      }
    },
    {
      "dokumentnummer": "1000027512",
      "type": "rettsstiftelsestype.rek",
      "typeBeskrivelse": "Åpning av rekonstruksjonsforhandling",
      "status": "statusregistreringsobjekt.sl",
      "statusBeskrivelse": "slettet",
      "innkomsttidspunkt": "2022-10-01T12:00:00+02:00",
      "beslutningstidspunkt": "2022-10-03T12:00:00+02:00",
      "slettet": "2023-03-06",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.domstol",
          "rolletypeBeskrivelse": "Domstol",
          "rollegruppetype": "rollegruppe.oppr",
          "rollegruppetypeBeskrivelse": "Oppretter",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "811086282"
          }
        },
        {
          "rolletype": "rolletype.rekonstruktoer",
          "rolletypeBeskrivelse": "Rekonstruktør",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.annenaktor",
            "navn": "Adv. Eva Testing"
          }
        },
        {
          "rolletype": "rolletype.skyldner",
          "rolletypeBeskrivelse": "Skyldner",
          "rollegruppetype": "rollegruppe.anro",
          "rollegruppetypeBeskrivelse": "Annen rolle",
          "rolleinnehaver": {
            "aktorType": "aktortype.person",
            "personnavn": {
              "fornavn": "EGOISTISK",
              "etternavn": "TROST"
            },
            "fodselsnummerEllerDNummer": "22866398228"
          }
        }
      ],
      "formuesgode": [],
      "prioritetsvikelse": []
    }
  ]
}
```

---

## Feilmeldinger

Dersom man ikke får HTTP-status 200, så får man en melding fra tjenesten i JSON-format.

| HTTP-kode   | Feilmelding                                                                                 |
|:----------- |:------------------------------------------------------------------------------------------- |
| 403         | Feil under autentisering av abonnent                                           |

##### Eksempelrespons feilmelding

```json
{
  "korrelasjonsid": "abd970cf-dae9-45cc-a9af-2011e512f96b",
  "tidspunkt": "2023-04-17T09:18:39.931121+02:00",
  "feilmelding": "lowerCutoff kan ikke være mer enn 30 dager tilbake i tid"
}
```

---
