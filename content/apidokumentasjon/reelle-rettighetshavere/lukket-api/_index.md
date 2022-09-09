---
title: Lukket API
description: Beskrivelse av Lukket API innen domene Reelle rettighetshavere
weight: 100
---

## Innledning
Tjenesten tilbyr oppslag på organisasjonsnummer som gir informasjon om reelle rettighetshavere inklusive fødselsnummer gjennom et lukket API.

## API-referanse

Denne tjenesten tilbyr opplysninger om:

* Reelle rettighetshavere inklusive fødselsnummer
 
[Lenke til Swagger](https://reelle-partner-api.apps.ocp-st.regsys.brreg.no/swagger-ui/index.html#/reelle%20rettigheter/hentReellRettighet) (Har de tilgang til Swagger?)

[Swagger-dokumentasjon](https://raw.githubusercontent.com/brreg/openAPI/master/specs/reelle-partner-api.yaml)
(last ned [Swagger-UI](https://github.com/swagger-api/swagger-ui) og utforsk linken)


## Sikkerhetsmekanismer
Siden dette er et begrensede API så skal kallende parter autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_guide_apikonsument.html).

For å kunne få tilgang til våre begrensede API er det tre forutsetninger.

1. Virksomhetssertifikat
2. Registrert klient hos Maskinporten.
3. JWT-token fra Maskinporten mot scopet `brreg:losore/utlegg`

Tokenet som hentes fra Maskinporten må bli sendt som autorisasjonstoken (Bearer token) når et kall mot Løsøreregisteret blir utført.

Se [veiledning for integrasjon mot Maskinporten]({{<ref "mp-integrasjonsveiledning.md">}}).

[Regelverk](https://lovdata.no/dokument/SF/forskrift/2015-12-11-1668/%C2%A76): Hjemler for tilgjengeliggjøring av data fra Brønnøysundregistrene.


## Grensesnittbeskrivelse

**Domener**:

* For testmiljø (ppe): `https://reelle-partner-api.apps.ocp-ppe.regsys.brreg.no`
* For prod: `https://reelle-partner-api.brreg.no` ?

### Oppslag på fødselsnummer/d-nummer

#### Beskrivelse

Tjenesten tar imot en forespørsel om oppslag på et organisasjonsnummer, forespørselen valideres før utførelsen og returnerer opplysninger om rettighetshavere inklusive fødselsnummer på oppgitt organisasjonsnummer.

#### Request

Tar i mot et organisasjonsnummer som en del av URL, med obligatorisk path-parameter `organisasjonsnummer` som det søkes på.

#### Validering

* Forespørselen skal alltid inneholde organisasjonsnummeret det gjøres oppslag på.
* Dersom forespørselen inneholder et organisasjonsnummer som ikke er lovlig oppbygd, returneres det en feilmelding.
* Det sjekkes at organisasjonsnummeret er registrert og ikke slettet i Enhetsregisteret. Dersom det ikke er registrert, eller er slettet, returneres det en feilmelding.

#### Response

Dersom kallet lykkes får man HTTP-status 200 og data fra tjenesten på JSON-format, i form av et JSON-objekt som inneholder opplysninger om rettighetshaver.

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

| HTTP-kode                 | Beskrivelse |
|:------------------------- |:----------- |
| 200 OK                    | Henting av data gikk bra |
| 400 Bad Request           | Feil i spørring. Applikasjonen vil gi en detaljert feilmelding for hva som er feil med spørring |
| 403 Forbidden             | Feil ved autentisering eller autorisering. Bearer tokenet som ble sendt inn er ikke gyldig eller har ikke en gyldig avtale om utlegg |
| 404 Not Found             | Applikasjonen vil gi en detaljert feilmelding for hva som ikke ble funnet. Kan også bety at man bruker feil adresse for tjenesten (i så fall vil man få en standard "404 NOT FOUND" og ikke et svar fra applikasjonen) |
| 500 Internal Server Error | Feil på server side, for eksempel at en underliggende datakilde ikke svarer |

## Ordliste

Definisjoner på begrep som er brukt i denne dokumentasjonen.

| Begrep | Definisjon |
|:------ |:---------- |
| API | Programmeringsgrensesnitt |
| HTTP | Datakommunikasjonsstandard |
| HTTP-statuskoder | Statuskoder for datakommunikasjonsstandard |
| REST | Datakommunikasjonmønster |
| JSON | Åpen standard for dataformat |
| Organisasjonsnummer | Identifikasjonsnummer for organisasjon |

---
