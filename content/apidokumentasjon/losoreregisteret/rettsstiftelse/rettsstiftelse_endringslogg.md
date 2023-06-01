---
title: Endringslogg
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 160
---

## Bruksmønster

Se [siden for totalbestand]({{<ref "rettsstiftelse_totalbestand.md">}}) for en helhetlig oversikt av bruksmønsteret for endringslogg og totalbestand.

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                   | Beskrivelse                                                                                  |
|:------------- |:------------------------------------------------------|:---------------------------------------------------------------------------------------------|
| POST          | https://\{domene\}/api/v2/rettsstiftelse/endringslogg?language={language} | Hent opplysninger endringer på rettsstiftelser fra et ønsket tidspunkt. Language er valgfri. |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Henting av endringslogg

#### Beskrivelse

Endepunktet tar imot en forespørsel med felter *lowerCutoff* for tidspunkt-avgrensning og *lastSortValues* for paginering.
Den valgfrie query parameteren "language" angir språkkode (ISO 639-2) for hvilket språk som skal benyttes for beskrivelser i responsen. Hvis den ikke er angitt benyttes norsk bokmål (NOB).

*Merk:* Kun rettsstiftelser nyere enn 30 dager vil inkluderes i responsen, uavhengig av om *lowerCutoff* settes før dette.

#### Validering

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens organisasjonsnummer, og dette organisasjonsnummeret skal være gyldig samt ha en gyldig avtale for å kunne hente ut opplysninger i Løsøreregisteret.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.
* Hvis "language" er angitt må verdien være en støttet språkkode, hvis ikke returneres det en feilmelding med informasjon om støttede språkkoder.

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
    "1685515741112",
    "1000009845"
  ]
}
```

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "sistEndretSisteInnslag": "2023-05-31T08:49:01.112334+02:00",
  "sortValues": [
    "1685515741112",
    "1000009845"
  ],
  "antallRettsstiftelser": 1,
  "rettsstiftelse": [
    {
      "dokumentnummer": "1000009845",
      "type": "rettsstiftelsestype.sap",
      "typeBeskrivelse": "Salgspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2022-11-11T08:00:00+01:00",
      "utlopRettsvernstid": "2042-11-11",
      "paategning": [],
      "rolle": [
        {
          "rolletype": "rolletype.panthaver",
          "rolletypeBeskrivelse": "Panthaver",
          "rollegruppetype": "rollegruppe.rett",
          "rollegruppetypeBeskrivelse": "Rettighetshaver",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810844612"
          }
        },
        {
          "rolletype": "rolletype.pantsetter",
          "rolletypeBeskrivelse": "Pantsetter",
          "rollegruppetype": "rollegruppe.forp",
          "rollegruppetypeBeskrivelse": "Forpliktet",
          "rolleinnehaver": {
            "aktorType": "aktortype.virksomhet",
            "organisasjonsnummer": "810845422"
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
              "fornavn": "PLUTSELIG",
              "etternavn": "MORMOR"
            },
            "fodselsnummerEllerDNummer": "13888998238"
          }
        }
      ],
      "formuesgode": [
        {
          "identifiseringsmate": "identifiseringsmate.entydig",
          "type": "formuesgodetype.mv.e",
          "typeBeskrivelse": "Registrert motorvogn",
          "eierandel": {},
          "registreringsnummerMotorvogn": "CU11242",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 105158028,
            "valuta": "NOK"
          }
        ],
        "kravSalgspant": "kravsalgspant.selgers.krav",
        "kravSalgspantBeskrivelse": "selgerens krav på kjøpesummen"
      }
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
