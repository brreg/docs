---
title: Totalbestand
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 150
---

## Bruksmønster

Tjenestene for å hente alle rettsstiftelser, og abonnere på endringene er delt inn i totalbestand og endringslogg. Totalbestand er endepunktet man bruker for å hente hele den aktive bestanden opp til og med et bestemt tidspunkt.
Når man har hentet alt som var tilgjengelig fra totalbestanden skal man bruke endringslogg endepunktet for å lytte på endringer i datasettet. Av denne grunn er tjenesten avgrenset slik at man med endringsloggen kun kan hente rettsstiftelser
som ble prosessert iløpet av de siste 30 dagene.

## Stegvis fremgangsmåte for å hente og vedlikeholde bestanden:

1. Kall totalbestand endepunktet med *"upperCutoff"* med tidspunkt da hentingen ble påbegynt, paginer igjennom resultatene som vist nedenfor.
2. Når man mottar en tom page har man hele totalbestanden opp til tidspunktet, ta med tidspunktet brukt i *"upperCutOff"* til bruk i endringslogg.
3. Kall endringslogg med feltet *"lowerCutoff"* satt til dette tidspunktet, paginer igjennom på tilsvarende måte.
4. Når man når tom side har man endringsloggen frem til nå. Ta vare på feltet *sistEndretSisteInnslag* fra siste page.
5. Vent til man ønsker å hente endringslogg igjen, og gjenta fra steg 3.

## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                   | Beskrivelse                                                                   |
|:------------- |:------------------------------------------------------|:------------------------------------------------------------------------------|
| POST          | https://\{domene\}/api/v2/rettsstiftelse/totalbestand | Hent alle opplysninger om aktive rettstiftelser opp til et ønsket tidspunkt   |

**Domener**:

* For testmiljø (ppe) `https://losoreregisteret.ppe.brreg.no/registerinfo`
* For produksjon `https://losoreregisteret.brreg.no/registerinfo`

### Henting av totalbestand

#### Beskrivelse

Tjenesten tar imot en forespørsel med feltene *upperCutOff* for tidspunkt-avgrensning og *lastSortValues* for paginering.

#### Validering

* Maskinport-tokenet som blir sendt inn er knyttet til avtalepartens organisasjonsnummer, og dette organisasjonsnummeret skal være gyldig samt ha en gyldig avtale for å kunne hente ut opplysninger i Løsøreregisteret.
* Avgrensningsverdien *upperCutoff* i request-body er en timestamp med tidssone på formatet "YYYY-MM-DDTHH:MM:SS.mmm+HH:MM", det valideres at feltet ikke peker frem i tid.
* Det sjekkes at avtalepartens organisasjonsnummer er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.

## Paginering

Grunnet store datamengder er det nødvendig å paginere requests og respons til tjenesten. Dette gjøres ved hjelp av feltet *"lastSortValues"*.
Ved første forespørsel skal dette feltet være *null*, deretter skal det settes til verdien til feltet *"sortValues"* i responsen fra forrige request.
Dette gjør at tjenesten er istand til å vite hvilken side av datasettet den skal returnere.

*Merk:* Siste side vil ha 0 rettsstiftelser, og vil ikke inneholde *"sortValues"*.

#### Request
Første request før paginering vil kunne se slik ut:
```json
{
  "upperCutoff": "2023-03-06T00:00:00.000+02:00",
  "lastSortValues": null
}
```
Deretter vil man, basert på *"sortValues"* fra forrige [response](#eksempelrespons), utforme en request som dette:
```json
{
    "upperCutoff": "2023-03-06T00:00:00.000+02:00",
    "lastSortValues": [
      "1675889424135",
      "38068529-7a2d-42d3-971a-b305c9adf801"
    ]
}
```

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettsstiftelsene.

##### Eksempelrespons

```json
{
  "upperCutoffForrigeRequest": "2023-03-05T22:00:00Z",
  "sortValues": [
    "1675889424135",
    "38068529-7a2d-42d3-971a-b305c9adf801"
  ],
  "antallRettsstiftelser": 1000,
  "rettsstiftelser": [
    {
      "dokumentnummer": "1000007302",
      "type": "rettsstiftelsestype.sap",
      "typeBeskrivelse": "Salgspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2022-11-11T07:00:00Z",
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
          "registreringsnummerMotorvogn": "CU11240",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 235572728.00,
            "valuta": "NOK"
          }
        ],
        "kravSalgspant": "kravsalgspant.selgers.krav",
        "kravSalgspantBeskrivelse": "selgerens krav på kjøpesummen"
      }
    },
    {
      "dokumentnummer": "1000007301",
      "type": "rettsstiftelsestype.sap",
      "typeBeskrivelse": "Salgspant",
      "status": "statusregistreringsobjekt.tl",
      "statusBeskrivelse": "tinglyst",
      "innkomsttidspunkt": "2022-11-11T07:00:00Z",
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
          "registreringsnummerMotorvogn": "CU11240",
          "historiskRegistreringsnummerMotorvogn": []
        }
      ],
      "prioritetsvikelse": [],
      "krav": {
        "belop": [
          {
            "belop": 1556438453.00,
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

| HTTP-kode   | Feilmelding                                                                                |
|:----------- |:-------------------------------------------------------------------------------------------|
| 400         | Totalbestand kan ikke hentes med upperCutoff frem i tid.                                   |
| 403         | Forespørsel inneholder ingen gyldig bearer token                                           |

##### Eksempelrespons feilmelding

```json
{
  "korrelasjonsid": "cba2c68f-2f04-4104-9dbf-8e69c5e36c5c",
  "tidspunkt": "2023-03-07 13:23:35",
  "feilmelding": "upperCutOff kan ikke peke frem i tid"
}
```

---
