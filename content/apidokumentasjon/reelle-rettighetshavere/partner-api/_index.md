---
title: Partner API
description: Beskrivelse av partner API for Register over reelle rettighetshavere
weight: 100
---

## Innledning
Det begrensede API'et tilbyr oppslag på organisasjonsnummer som gir informasjon om reelle rettighetshavere inklusive fødselsnummer.

## API-referanse

Denne tjenesten tilbyr opplysninger om fysiske personer som er reelle rettighetshavere i virksomheten, samt hvilke reelle rettigheter disse har, inklusive fødselsnummer og d-nummer.
 
[Lenke til Swagger](https://reelle-partner-api.apps.ocp-prd.regsys.brreg.no/swagger-ui/index.html#/reelle%20rettigheter/hentReellRettighet) (Har de tilgang til Swagger?)

[Swagger-dokumentasjon](https://raw.githubusercontent.com/brreg/openAPI/master/specs/reelle-partner-api.yaml)
(last ned [Swagger-UI](https://github.com/swagger-api/swagger-ui) og utforsk linken)


## Sikkerhetsmekanismer
Siden dette er et Partner API skal kallende parter autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_guide_apikonsument.html).

For å kunne få tilgang til våre begrensede API er det tre forutsetninger.

1. Virksomhetssertifikat
2. Registrert klient hos Maskinporten.
3. I dialogen med Brønnøysundregistrene om å få tilgang til API'et vil din virksomhet ha fått informasjon om hvilket av de to scopene virksomheten har fått tilgang til.
JWT-token fra Maskinporten mot ett av disse scopene:
   1. `brreg:reelle/partner.offentlig`
   2. `brreg:reelle/partner.rapporteringspliktig`

Tokenet som hentes fra Maskinporten må bli sendt som autorisasjonstoken (Bearer token) når et kall mot tjenesten blir utført.

Se [veiledning for integrasjon mot Maskinporten]({{<ref "mp-integrasjonsveiledning.md">}}).

[Regelverk](https://lovdata.no/dokument/SF/forskrift/2021-06-21-2056?q=forskrift%20reelle%20rettighetshavere): Hjemler for tilgjengeliggjøring av data fra Brønnøysundregistrene.


## Grensesnittbeskrivelse

| HTTP-metode   | URL                                                                                                    | Beskrivelse                                                                            |
|:------------- |:-------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------|
| GET           | https://\{domene\}/rrh/api/reelle-rettighetshavere/{organisasjonsnummer}                               | Hent opplysninger om reell rettighetshaver på gitt organisasjonsnummer. |

**Domener**:

* For testmiljø (ppe): `https://reelle-partner-api.apps.ocp-ppe.regsys.brreg.no`
* For prod: `https://reelle-partner-api.brreg.no` ?

### Oppslag på organisasjonsnummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer. Forespørselen valideres og returnerer opplysninger om reelle rettighetshavere inklusive fødselsnummer/d-nummer på oppgitt organisasjonsnummer.

#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.

#### Validering

* Forespørselen skal alltid inneholde organisasjonsnummeret det gjøres oppslag på.
* Dersom forespørselen inneholder et organisasjonsnummer som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at organisasjonsnummeret er registrert i Enhetsregisteret. Dersom det ikke er registrert returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 samt et dokument (på JSON-format) i retur. JSON-dokumentet inneholder opplysninger om reelle rettighetshavere.

<details><summary>**Eksempelrespons**</summary><p>

##### Eksempelrespons for oppslag på organisasjonsnummer

```json
{
  "registreringId": "6f2baebd-44bc-47dc-9a1e-d9131a4219be",
  "registreringStatus": {
    "kode": "registreringstatus.regi",
    "beskrivelse": null
  },
  "gjelderFraDato": "2022-08-25T11:18:03.423645Z",
  "reelleRettighetshavereStatus": {
    "kode": "reellerettighetshaverestatus.arid",
    "beskrivelse": null
  },
  "reelleRettighetshavere": [
    {
      "foedselsdato": "1982-03-23",
      "foedselsaar": "1982",
      "navn": {
        "fornavn": null,
        "mellomnavn": null,
        "etternavn": null,
        "fulltNavn": "Dansk Danskesen"
      },
      "foerstRegistrertDato": "2022-08-19T12:28:06.674996Z",
      "endretDato": "2022-08-25T11:18:01.231688Z",
      "statsborgerskap": [
        {
          "landkode": "DK",
          "land": null
        }
      ],
      "bostedsland": {
        "landkode": "DK",
        "land": null
      },
      "erDoed": null,
      "erUnntattFraInnsyn": null,
      "posisjoner": [
        {
          "posisjonType": {
            "kode": "posisjontype.eier",
            "beskrivelse": null
          },
          "stoerrelseIntervall": {
            "kode": "stoerrelseintervall.int3",
            "beskrivelse": null
          },
          "grunnlag": [
            {
              "grunnlagType": {
                "kode": "grunnlagtype.dire",
                "beskrivelse": null
              }
            }
          ],
          "beskrivelseAnnenMaate": null
        }
      ]
    },
    {
      "foedselsdato": "1973-03-22",
      "foedselsaar": "1973",
      "navn": {
        "fornavn": null,
        "mellomnavn": null,
        "etternavn": null,
        "fulltNavn": "Svensk Svenskesen"
      },
      "foerstRegistrertDato": "2022-08-25T11:18:01.231688Z",
      "endretDato": "2022-08-25T11:18:01.231688Z",
      "statsborgerskap": [
        {
          "landkode": "NO",
          "land": null
        }
      ],
      "bostedsland": {
        "landkode": "NO",
        "land": null
      },
      "erDoed": null,
      "erUnntattFraInnsyn": null,
      "posisjoner": [
        {
          "posisjonType": {
            "kode": "posisjontype.eier",
            "beskrivelse": null
          },
          "stoerrelseIntervall": {
            "kode": "stoerrelseintervall.int2",
            "beskrivelse": null
          },
          "grunnlag": [
            {
              "grunnlagType": {
                "kode": "grunnlagtype.dire",
                "beskrivelse": null
              }
            }
          ],
          "beskrivelseAnnenMaate": null
        }
      ]
    }
  ]
}
```

---

</p></details>

## HTTP-statuskoder

| HTTP-kode                 | Beskrivelse                                                                                                                                                                          |
|:--------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200 OK                    | Henting av data gikk bra                                                                                                                                                             |
| 400 Bad Request           | Feil i spørring. Applikasjonen vil gi en detaljert feilmelding for hva som er feil med spørring                                                                                      |
| 403 Forbidden             | Feil ved autentisering eller autorisering. Bearer-tokenet som ble sendt inn er ikke gyldig eller virksomheten har ikke fått tilgang til scope for tjenesten                          |
| 403 Not Found             | Virksomheten har ikke registrert reelle rettighetshavere                                                                                                                             |
| 404 Not Found             | Virksomheten ikke er registreringspliktig i register over reelle rettighetshavere                                                                                                    |
| 500 Internal Server Error | Intern feil i tjenesten, for eksempel at en underliggende datakilde ikke svarer                                                                                                      |

## Ordliste

Definisjoner på begrep som er brukt i denne dokumentasjonen.

| Begrep              | Definisjon                                                                           |
|:--------------------|:-------------------------------------------------------------------------------------|
| API                 | Programmeringsgrensesnitt                                                            |
| Partner API         | Et API som krever autentisering/autorisering (for eksempel ved bruk av Maskinporten) |
| HTTP                | Datakommunikasjonsstandard                                                           |
| HTTP-statuskoder    | Statuskoder for datakommunikasjonsstandard                                           |
| REST                | Datakommunikasjonmønster                                                             |
| JSON                | Åpen standard for dataformat                                                         |
| Organisasjonsnummer | Identifikasjonsnummer for virksomhet                                                 |

---
