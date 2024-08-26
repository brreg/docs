---
title: Innsending av Altinn-skjema
description: Beskrivelse av hvordan man sender inn registreringer som tredjeleverandør.
weight: 100
---

Som sluttbrukersystem kan du sende inn opplysninger om Reelle rettighetshavere til oss ved å følge stegene på denne siden:
<!-- TOC -->
  * [Sekvensdiagram](#sekvensdiagram)
  * [ID-Porten](#id-porten)
    * [1. Send sluttbruker til ID-Porten](#1-send-sluttbruker-til-id-porten)
  * [Veksle inn Altinn-token](#veksle-inn-altinn-token)
    * [2. Veksle inn ID-Porten-tokenet til et Altinn-token](#2-veksle-inn-id-porten-tokenet-til-et-altinn-token)
  * [API-kall mot Altinn App API](#api-kall-mot-altinn-app-api)
    * [3. Hent partyId til virksomheten](#3-hent-partyid-til-virksomheten)
    * [4. Hent preutfylte skjemadata](#4-hent-preutfylte-skjemadata)
    * [5. Bygg opplysninger om Reelle rettighetshavere som JSON i ditt system](#5-bygg-opplysninger-om-reelle-rettighetshavere-som-json-i-ditt-system)
    * [6. Opprett en instans av våre skjemadata](#6-opprett-en-instans-av-våre-skjemadata)
    * [7. Oppdater skjemadata med sluttbrukers endringer (som du bygget opp i steg 5.)](#7-oppdater-skjemadata-med-sluttbrukers-endringer-som-du-bygget-opp-i-steg-5)
    * [8. Gå til neste prosessteg](#8-gå-til-neste-prosessteg)
    * [9. Valider og send inn skjema](#9-valider-og-send-inn-skjema)
<!-- TOC -->


## Sekvensdiagram

![Sekvensdiagram - Innsending av Altinn-skjema til Register over reelle rettighetshavere](sekvensdiagram_minn.png)

## ID-Porten

### 1. Send sluttbruker til ID-Porten

For at ditt system skal få lov til å sende inn registrering av reelle rettighetshavere inn til oss må din sluttbruker
autentisere seg gjennom ID-Porten.
Vi anbefaler at du
følger [Digdirs integrasjonsguide for autentisering i ID-Porten](https://docs.digdir.no/docs/idporten/oidc/oidc_guide_idporten.html).

Når du følger guiden må du gjøre følgende steg:

1. Sende en autentiseringsforespørsel til autorisasjons-endepunktet
    * **Her må du også legge til et query-param `scope` med verdi `altinn:instances.write`**. Denne trenger du for å få
      lov til å gjøre CRUD-forespørsler mot Altinns APP API.
2. Bruker autentiserer seg på sin foretrukkende måte, feks BankId. Sluttbruker må også godkjenne at ditt
   sluttbrukersystem får tilgang scope `altinn:instances.write` på vegne at sluttbruker.
3. Bruker blir redirected tilbake til din tjeneste
4. Du kaller token-endepunktet og utsteder et ID-Porten-token.

{{< expandableCode title="Eksempel på et B64-encoded ID-Porten-token" lang="text">}}
eyJraWQiOiJkaWdpdGFsaXNlcmluZ3NkaXJla3RvcmF0ZXQtLWNlcnQwIiwiYWxnIjoiUlMyNTYifQ.eyJzdWIiOiIxOTg1NTQ5NzkyNCIsImFjciI6ImlkcG9ydGVuLWxvYS1zdWJzdGFudGlhbCIsInNjb3BlIjoiYWx0aW5uOmluc3RhbmNlcy53cml0ZSIsImlzcyI6Imh0dHBzOi8vdGVzdC5pZHBvcnRlbi5ubyIsImNsaWVudF9hbXIiOiJjbGllbnRfc2VjcmV0X3Bvc3QiLCJwaWQiOiIxOTg1NTQ5NzkyNCIsImV4cCI6MTcxODEwMzY4MywiaWF0IjoxNzE4MTAzMDgzLCJqdGkiOiIyMEszRHVaSWRrQSIsImNsaWVudF9pZCI6Ijk3YWMzMjg2LTU3ZWQtNDMzMy05ODU5LTdkMGE4NTIzZTdmZiIsImNvbnN1bWVyIjp7ImF1dGhvcml0eSI6ImlzbzY1MjMtYWN0b3JpZC11cGlzIiwiSUQiOiIwMTkyOjk3NDc2MDY3MyJ9fQ.Lvi--jq2GuM3VEb3K8aFFJZqzqSewHMmHqap6eV7Bibl3nZ9dTWTUhrkNIr4ZSHZkBvIk-A6DcnF8L47rvJVgmN0kczJDVXCv1E8W3yu5mA57k0uvZIxXW0paH6ldQZ2vJL_3iyhg9GLmiU-He5JTtwo_ULo0VX6DVt97lhVf_WHrLY9steIW82ujeMY3m-qUbgRTT9h1LAITpfpX8Mavk1B4gDwzYYx-6S2VNUOMo72b466mAM5-4JUejpPLwCpAr2LNT7pgEh8p8cxHGj0cKNpJ_nqbp7Awc2tJSpYS53YgMIwaYiZA5oKWvVc6RTTx0GgQrHL2IMnK2ObHIBmCPH2vKjwYpZQUBwkXCglxlxdTn9lMmYzA3fLCrQKt_SRDL9GoAjLjgz_h-E0N-hVpBsRJY_K_xgPbqdanhG6pTE352uwuaTVAUpAISRHA-So6yFm2A1Pq-sN5FBpjF6s6KFWmXz3Ro6YXEhWCiuJHkl-GdEnHGq026L3JpNddpmJ
{{< /expandableCode >}}

For å se innholdet til et slikt token kan du B64-decode det, eller bruke verktøy, feks https://jwt.io/.

{{< expandableCode title="Eksempel på et ID-Porten-token etter decoding" lang="json" >}}
{
  "sub": "19855497924",
  "acr": "idporten-loa-substantial",
  "scope": "altinn:instances.write",
  "iss": "https://test.idporten.no",
  "client_amr": "client_secret_post",
  "pid": "19855497924",
  "exp": 1718103683,
  "iat": 1718103083,
  "jti": "20K3DuZIdkA",
  "client_id": "97ac3286-57ed-4333-9859-7d0a8523e7ff",
  "consumer": {
    "authority": "iso6523-actorid-upis",
    "ID": "0192:974760673"
  }
}
{{< /expandableCode >}}

## Veksle inn Altinn-token

### 2. Veksle inn ID-porten-tokenet til et Altinn-token

For å veksle inn Altinn-tokenet må du sette følgende header:

* `ApiKey` Du må legge inn ApiKey-en som du fikk når du bestilte tilgang til Altinns REST-APIer.
* `Authorization`: Her må du legge til ID-Porten-tokenet du ustedte fra ID-Porten. Siden dette er et Bearer-token skal
* `Authorization`: Her må du legge til ID-porten-tokenet du ustedte fra ID-porten. Siden dette er et Bearer-token skal
  verdien av tokenet være: `Bearer <<idporten access_token>>`

ID-Porten-tokenet kan veksles inn ved å kalle Altinns exchange-endepunkt:

* `GET {{altinn-miljø}}/authentication/api/v1/exchange/id-porten`

Du får nå et Altinn-token som du skal bruke i alle resterende kall.

{{< expandableCode title="Eksempel på respons (B64-encoded token)" >}}
eyJhbGciOiJSUzI1NiIsImtpZCI6IjM4QUE3QTc5MjUzNDNCQjE0NjFCRUUwMURCNUQwOTRBM0VCOTgwMjUiLCJ4NXQiOiJPS3A2ZVNVME83RkdHLTRCMjEwSlNqNjVnQ1UiLCJ0eXAiOiJKV1QifQ.eyJuYW1laWQiOiIxNjE0ODgiLCJ1cm46YWx0aW5uOnVzZXJpZCI6IjE2MTQ4OCIsInVybjphbHRpbm46dXNlcm5hbWUiOiIiLCJ1cm46YWx0aW5uOnBhcnR5aWQiOjUwNzE0MjM4LCJ1cm46YWx0aW5uOmF1dGhlbnRpY2F0ZW1ldGhvZCI6Ik5vdERlZmluZWQiLCJ1cm46YWx0aW5uOmF1dGhsZXZlbCI6MywiYWNyIjoiaWRwb3J0ZW4tbG9hLXN1YnN0YW50aWFsIiwic2NvcGUiOiJhbHRpbm46aW5zdGFuY2VzLndyaXRlIiwiY2xpZW50X2FtciI6ImNsaWVudF9zZWNyZXRfcG9zdCIsInBpZCI6IjE5ODU1NDk3OTI0IiwiZXhwIjoxNzE4MTAzNjgzLCJpYXQiOjE3MTgxMDMzNjQsImNsaWVudF9pZCI6Ijk3YWMzMjg2LTU3ZWQtNDMzMy05ODU5LTdkMGE4NTIzZTdmZiIsImNvbnN1bWVyIjp7ImF1dGhvcml0eSI6ImlzbzY1MjMtYWN0b3JpZC11cGlzIiwiSUQiOiIwMTkyOjk3NDc2MDY3MyJ9LCJpc3MiOiJodHRwczovL3BsYXRmb3JtLnR0MDIuYWx0aW5uLm5vL2F1dGhlbnRpY2F0aW9uL2FwaS92MS9vcGVuaWQvIiwianRpIjoiMjZmNGE4ZTEtMzk3Ny00ODI3LTgwYmYtYTE3MzhiMjU0OTI1IiwibmJmIjoxNzE4MTAzMzY0fQ.gK3Dpnx8mZbnT-WQZBFtzRfxNkVwlLftuO1hi6uB1nH91nJRRVxPQbEn4JADe1SFrpQEtz9BFyXXhdrs-uuGp3AIRBdgyQsXEM6lziX8L7pe1Dwee5CujfP56INAGgxcchn2HJNjI1tdSIepfDv225-aQRIbc9EF-2wyenqaT-G7EhDKVPpr_uiRctXBDIqlJJxlaLhBWpl7VZvMUh5JXlqQGkXl_SLMLR9pI7BpeFrTGwWJTKRQu90dSPKflnBU8-VIXn8tvQRY4-mnO-IbvBe3cLbiH64tBkzs_9bhpLOsTDnpVdcEq18f-_Wji4wq-MRF1q1VnXLbDcru5ST-Lg
{{< /expandableCode >}}

{{< expandableCode title="Eksempel decodet token" lang="json" >}}
{
  "nameid": "161488",
  "urn:altinn:userid": "161488",
  "urn:altinn:username": "",
  "urn:altinn:partyid": 50714238,
  "urn:altinn:authenticatemethod": "NotDefined",
  "urn:altinn:authlevel": 3,
  "acr": "idporten-loa-substantial",
  "scope": "altinn:instances.write",
  "client_amr": "client_secret_post",
  "pid": "19855497924",
  "exp": 1718103683,
  "iat": 1718103364,
  "client_id": "97ac3286-57ed-4333-9859-7d0a8523e7ff",
  "consumer": {
    "authority": "iso6523-actorid-upis",
    "ID": "0192:974760673"
  },
  "iss": "https://platform.tt02.altinn.no/authentication/api/v1/openid/",
  "jti": "26f4a8e1-3977-4827-80bf-a1738b254925",
  "nbf": 1718103364
}
{{< /expandableCode >}}

## API-kall mot Altinn App API

**I alle videre API-kall mot Altinn må du sette følgende header:**

* `Authorization`: Her må du legge til **Altinn-tokenet** vekslet inn. Siden dette er et Bearer-token skal verdien av
  tokenet være: `Bearer <<altinn-token>>`

{{< warning >}}
Husk at du må sette denne headeren i alle kallene nedenfor.
{{< /warning >}}

### 3. Hent partyId til virksomheten

Sluttbruker kan opptre på vegne av en til mange Parties i Altinn. Du må hente ut partyId til virksomheten du skal sende
inn registrering for.

* `GET {{altinn-miljø}}/brg/rrh-innrapportering/api/v1/parties`

Du får en liste med Parties som bruker kan opptre på vegne av. Her kan du sjekke at feltet "orgNumber" samsvarer med
organisasjonsnummeret du skal sende inn for. Du trenger partyId i alle resterende kall.

{{< expandableCode title="Eksempel på respons (Hent partyId)" lang="json" >}}
[
    {
        "partyId": 51609308,
        "partyUuid": "c74c96f1-494d-4600-866e-3c8de4748466",
        "partyTypeName": 2,
        "orgNumber": "310956643",
        "ssn": null,
        "unitType": "AS",
        "name": "GEOMETRISK VEIK TIGER AS",
        "isDeleted": false,
        "onlyHierarchyElementWithNoAccess": false,
        "person": null,
        "organization": null,
        "childParties": [
            {
                "partyId": 51977240,
                "partyUuid": "17f4cdd0-c58b-49fd-8857-8485a944e881",
                "partyTypeName": 2,
                "orgNumber": "315220521",
                "ssn": null,
                "unitType": "BEDR",
                "name": "GEOMETRISK VEIK TIGER AS",
                "isDeleted": false,
                "onlyHierarchyElementWithNoAccess": false,
                "person": null,
                "organization": null,
                "childParties": null
            }
        ]
    },
    {
        "partyId": 50555707,
        "partyUuid": "da990f35-d8fa-416f-baf6-02935fc10f4c",
        "partyTypeName": 1,
        "orgNumber": "",
        "ssn": "01812647772",
        "unitType": null,
        "name": "JULEPRESANG FALSK",
        "isDeleted": false,
        "onlyHierarchyElementWithNoAccess": false,
        "person": null,
        "organization": null,
        "childParties": null
    }
]
{{< /expandableCode >}}

### 4. Hent preutfylte skjemadata

For å forenkle prosessen med å sende inn opplysninger om reelle rettighetshavere vil skjemainstansen være preutfylt med 
data fra registeret. Hvis du tidligere har sendt inn opplysninger vil disse komme som en del av preutfyllingen. Hvis du 
ikke har sendt inn opplysninger tidligere vil du likevel få en begrenset preutfylling tilbake som stort sett bare 
består av noen metadata-felter.

`GET {{altinn-miljø}}/brg/rrh-innrapportering/prefill/{partyId}`

{{< expandableCode title="Respons for en virksomhet som ikke har sendt inn registrering tidligere" lang="json" >}}
{
    "versjon": "1.0.0",
    "endret": "2024-08-12",
    "skjemainnhold": {
        "metadata": {
            "tjeneste": "rrh.ktr.reelle",
            "tjenestehandling": "nyregistrering",
            "rettighetsinformasjonsid": "RRH202200000008"
            "registreringsid": "1af8df28-1bf4-4f5c-92cd-6b1ecedb2c61"
        },
        "integrasjon": {
            "hfHentPreutfyllingFeilet": false,
            "hfHentRollerFeilet": null
        }
    }
}
{{< /expandableCode >}}


{{< expandableCode title="Respons for en virksomhet som har sendt inn registrering tidligere" lang="json" >}}
{
    "versjon": "1.0.0",
    "endret": "2024-08-12",
    "skjemainnhold": {
        "metadata": {
            "tjeneste": "rrh.ktr.reelle",
            "tjenestehandling": "endring",
            "rettighetsinformasjonsid": "RRH202400000182",
            "registreringsid": "172ebaee-7eb2-491f-a140-d469430d3c98"
        },
        "fagsystem": {
            "organisasjonsnummer": null,
            "navn": null
        },
        "integrasjon": {
            "hfHentPreutfyllingFeilet": false,
            "hfHentRollerFeilet": null
        },
        "skjemadata": {
            "registreringspliktigVirksomhet": {
                "organisasjonsnummer": "310956643",
                "hfSoekOrganisasjonsnummerFeilkode": null,
                "hfNavn": "GEOMETRISK VEIK TIGER AS",
                "hfOrganisasjonsform": "AS",
                "hfForretningsadresse": null,
                "hfNavnPaaHovedvirksomhetRegistrertIEoes": null,
                "hfLandnavnForHovedvirksomhetRegistrertIEoes": null,
                "hfSoekPaaOrganisasjonsnummer": null
            },
            "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
            "aarsakTilAtVirksomhetIkkeHarReelleRettighetshavere": null,
            "finnesDetReelleRettighetshavereITilleggTilRolleinnehavereForStiftelse": null,
            "reellRettighetshaver": [
                {
                    "erRegistrertIFolkeregisteret": true,
                    "hfErPreutfylt": true,
                    "folkeregistrertPerson": {
                        "foedselsEllerDNummer": "41864000647",
                        "hfFulltNavn": "HEVNGJERRIG SERVIETT",
                        "hfBostedsland": "UKJENT",
                        "hfStatsborgerskap": "Norge",
                        "hfSoekPaaEtternavn": null,
                        "hfSoekFeilkode": null,
                        "hfSoekPaaFoedselsEllerDNummer": null
                    },
                    "utenlandskPerson": null,
                    "hfFulltNavnTabellvisning": "HEVNGJERRIG SERVIETT",
                    "harPosisjonEierskap": true,
                    "posisjonEierskap": {
                        "stoerrelsesintervall": "stoerrelsesintervall.intervall2",
                        "grunnlag": "grunnlagstype.direkte",
                        "mellomliggendeVirksomhet": []
                    },
                    "harPosisjonKontrollOverStemmerettigheter": false,
                    "posisjonKontrollOverStemmerettigheter": null,
                    "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
                    "grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": null,
                    "harPosisjonKontrollPaaAnnenMaate": null,
                    "beskrivelseAvPosisjonenKontrollPaaAnnenMaate": null,
                    "harPosisjonAvgittGrunnkapital": false,
                    "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
                    "harPosisjonDestinatar": false,
                    "harPosisjonSaerligeRettigheter": false,
                    "hfPosisjonsbeskrivelseTabellvisning": "Eierskap 50% - 74,99%"
                }
            ],
            "kanIkkeIdentifisereFlereReelleRettighetshavere": true,
            "erVirksomhetRegistrertPaaRegulertMarked": null,
            "regulertMarked": null,
            "erReelleRettighetshavereRegistrertIUtenlandskRegister": null,
            "utenlandskRegister": null,
            "rolleinnehaver": null
        }
    }
}
{{< /expandableCode >}}

### 5. Bygg opplysninger om Reelle rettighetshavere som JSON i ditt system

JSON-skjema for å validere dataene dine er tilgjengelig på 
[https://schema.brreg.no/reelle/altinn/schema.json](https://schema.brreg.no/reelle/altinn/schema.json). Skjemaet kan benyttes til å validere endringer du gjør på
på de preutfylte datene ([steg 4.](#4-hent-preutfylte-skjemadata)).

Du kan finne JSON-eksempler sammen med en beskrivelse av hva som må fylles ut på denne [siden](../eksempler-paa-registrering).

For å teste hvordan ulike kombinasjoner av reelle rettighetshavere bygges opp, kan du også manuelt fylle disse ut i 
vårt Altinn-skjema på TT02. Etterpå kan du maskinelt hente ut preutfylte skjemadata ([steg 4.](#4-hent-preutfylte-skjemadata)), og se hvordan 
opplysningene ser ut i JSON. 

{{< info >}}
<strong>Selv om virksomheten ikke har innrapportert opplysninger om reelle rettighetshavere tidligere, må du alltid ta 
utgangspunkt i preutfylte data når du skal rapportere inn reelle rettighetshavere i ditt sluttbrukersystem!</strong><br> 
Feltene versjon og endret, samt innholdet i "metadata" som du rapporter inn <strong> må være identisk med innholdet du 
hentet fra de preutfylte dataene</strong>.
{{< /info >}}

Når du har ferdigstilt opplysningene som JSON kan du gå videre til neste steg.

### 6. Opprett en instans av våre skjemadata
{{< warning >}}
Hvis det har tatt tid å fylle ut opplysninger kan det hende at Altinn-tokenet har gått ut. Da må du gjenta steg 1. og 
steg 2., slik at du får et gyldig Altinn-token.
{{< /warning >}}

Med en ferdigstilt registrering kan du sende denne inn til oss.
Første steg er å opprette en instans av vårt Altinn-skjema. Dette gjør du med følgende API-kall:

`POST {{altinn-miljø}}/brg/rrh-innrapportering/instances?instanceOwnerPartyId={{partyId}}`
* Her må du bruke `partyId` som du hentet i steg 3.

I responsen får du UUID `skjema_instans_id` fra feltet `data.instanceGuid` og `skjema_instans_data_id` fra 
feltet `data.id`, som du må bruke i de påfølgende kallene.

{{< expandableCode title="Eksempel på respons" lang="json" >}}
{
  "id": "51543302/a1c8aea5-f236-49b4-9c8c-74797d14962b",
  "instanceOwner": {
    "partyId": "51543302",
    "personNumber": null,
    "organisationNumber": "310211036",
    "username": null
  },
  "appId": "brg/rrh-innrapportering",
  "org": "brg",
  "selfLinks": {
    "apps": "https://brg.apps.tt02.altinn.no/brg/rrh-innrapportering/instances/51543302/a1c8aea5-f236-49b4-9c8c-74797d14962b",
    "platform": "https://platform.tt02.altinn.no/storage/api/v1/instances/51543302/a1c8aea5-f236-49b4-9c8c-74797d14962b"
  },
  "dueBefore": null,
  "visibleAfter": "2024-07-29T06:31:13.2428807Z",
  "process": {
    "started": "2024-07-29T06:31:13.1826546Z",
    "startEvent": "BRStart",
    "currentTask": {
      "flow": 2,
      "started": "2024-07-29T06:31:13.1934811Z",
      "elementId": "TaskUtfylling",
      "name": "Utfylling",
      "altinnTaskType": "data",
      "ended": null,
      "validated": null,
      "flowType": "CompleteCurrentMoveToNext"
    },
    "ended": null,
    "endEvent": null
  },
  "status": {
    "isArchived": false,
    "archived": null,
    "isSoftDeleted": false,
    "softDeleted": null,
    "isHardDeleted": false,
    "hardDeleted": null,
    "readStatus": 1,
    "substatus": null
  },
  "completeConfirmations": null,
  "data": [
    {
      "id": "deeb1367-5686-4353-870d-93b4ac95befe",
      "instanceGuid": "a1c8aea5-f236-49b4-9c8c-74797d14962b",
      "dataType": "Brønnøysundregistrene_ReelleRettighetshavere_M",
      "filename": null,
      "contentType": "application/xml",
      "blobStoragePath": "brg/rrh-innrapportering/a1c8aea5-f236-49b4-9c8c-74797d14962b/data/deeb1367-5686-4353-870d-93b4ac95befe",
      "selfLinks": {
        "apps": "https://brg.apps.tt02.altinn.no/brg/rrh-innrapportering/instances/51543302/a1c8aea5-f236-49b4-9c8c-74797d14962b/data/deeb1367-5686-4353-870d-93b4ac95befe",
        "platform": "https://platform.tt02.altinn.no/storage/api/v1/instances/51543302/a1c8aea5-f236-49b4-9c8c-74797d14962b/data/deeb1367-5686-4353-870d-93b4ac95befe"
      },
      "size": 496,
      "contentHash": null,
      "locked": false,
      "refs": null,
      "isRead": true,
      "tags": [],
      "metadata": null,
      "deleteStatus": null,
      "fileScanResult": "NotApplicable",
      "references": null,
      "created": "2024-07-29T06:31:13.4397674Z",
      "createdBy": "161488",
      "lastChanged": "2024-07-29T06:31:13.439767Z",
      "lastChangedBy": "161488"
    }
  ],
  "presentationTexts": null,
  "dataValues": {},
  "created": "2024-07-29T06:31:13.2428807Z",
  "createdBy": "161488",
  "lastChanged": "2024-07-29T06:31:13.24288Z",
  "lastChangedBy": "161488"
}
{{< /expandableCode >}}


### 7. Oppdater skjemadata med sluttbrukers endringer (som du bygget opp i steg 5.)

Du må nå sette skjemadata som du opprettet i steg 5 på instansen. Dette gjør du ved å kalle dette endepunktet:
`PUT {{altinn-miljø}}/brg/rrh-innrapportering/instances/{{partyId}}/{{skjema_instans_id}}/data/{{skjema_instans_data_id}}?dataType=Brønnøysundregistrene_ReelleRettighetshavere_M`
* Her må du bruke `skjema_instans_id` og `skjema_instans_data_id` fra forrige API-kall.

{{< expandableCode title="Eksempel på respons" lang="json" >}}
{
    "changedFields": {
        "skjemainnhold.skjemadata.reellRettighetshaver[0].hfPosisjonsbeskrivelseTabellvisning": "Eierskap 75% - 100%"
    },
    "id": "31d4c79d-b121-478a-930e-4763b48194e6",
    "instanceGuid": "2381cb22-fec3-402f-82d8-08b31af7e7ff",
    "dataType": "Brønnøysundregistrene_ReelleRettighetshavere_M",
    "filename": null,
    "contentType": "application/xml",
    "blobStoragePath": "brg/rrh-innrapportering/2381cb22-fec3-402f-82d8-08b31af7e7ff/data/31d4c79d-b121-478a-930e-4763b48194e6",
    "selfLinks": {
        "apps": "https://brg.apps.tt02.altinn.no/brg/rrh-innrapportering/instances/51543302/2381cb22-fec3-402f-82d8-08b31af7e7ff/data/31d4c79d-b121-478a-930e-4763b48194e6",
        "platform": "https://platform.tt02.altinn.no/storage/api/v1/instances/51543302/2381cb22-fec3-402f-82d8-08b31af7e7ff/data/31d4c79d-b121-478a-930e-4763b48194e6"
    },
    "size": 2066,
    "contentHash": null,
    "locked": false,
    "refs": null,
    "isRead": true,
    "tags": [],
    "metadata": null,
    "deleteStatus": null,
    "fileScanResult": "NotApplicable",
    "references": null,
    "created": "2024-08-01T11:15:12.8774685Z",
    "createdBy": "161488",
    "lastChanged": "2024-08-01T11:15:19.851979Z",
    "lastChangedBy": "161488"
}
{{< /expandableCode >}}

### 8. Gå til neste prosessteg 

Du kan nå gå videre til neste prosessteg i Altinn, det fører til at skjemadataene klargjøres for innsending.
Du kan gå til neste prosessteg ved å kalle endepunktet:

`PUT {{altinn-miljø}}/brg/rrh-innrapportering/instances/{{party_id}}/{{skjema_instans_id}}/process/next`

{{< expandableCode title="Eksempel på respons" lang="json" >}}
{
    "currentTask": {
        "actions": {
            "read": true,
            "write": false,
            "confirm": true,
            "reject": true
        },
        "userActions": [
            {
                "id": "read",
                "authorized": true,
                "type": "ProcessAction"
            },
            {
                "id": "write",
                "authorized": false,
                "type": "ProcessAction"
            },
            {
                "id": "confirm",
                "authorized": true,
                "type": "ProcessAction"
            },
            {
                "id": "reject",
                "authorized": true,
                "type": "ProcessAction"
            }
        ],
        "read": true,
        "write": false,
        "flow": 3,
        "started": "2024-08-05T12:49:36.9688172Z",
        "elementId": "TaskBekreftelse",
        "name": "Bekreftelse",
        "altinnTaskType": "confirmation",
        "ended": null,
        "validated": null,
        "flowType": "CompleteCurrentMoveToNext"
    },
    "processTasks": [
        {
            "altinnTaskType": "data",
            "elementId": "TaskUtfylling"
        },
        {
            "altinnTaskType": "confirmation",
            "elementId": "TaskBekreftelse"
        }
    ],
    "started": "2024-08-05T12:48:19.5384915Z",
    "startEvent": "BRStart",
    "ended": null,
    "endEvent": null
}
{{< /expandableCode >}}

### 9. Valider og send inn skjema

Du kan nå validere og sende inn skjemadataene du har satt. Dette gjør du ved å kalle endepunktet:

`PUT {{altinn-miljø}}/brg/rrh-innrapportering/instances/{{party_id}}/{{skjema_instans_id}}/process/next?elementId=BREnd`
* Om skjemaet inneholder feil, vil du få en eller flere feilmeldinger i responsen (se eksempel under).

{{< expandableCode title="Eksempel på respons som er sendt inn" lang="json" >}}
{
    "currentTask": null,
    "processTasks": [
        {
            "altinnTaskType": "data",
            "elementId": "TaskUtfylling"
        },
        {
            "altinnTaskType": "confirmation",
            "elementId": "TaskBekreftelse"
        }
    ],
    "started": "2024-08-01T11:15:12.5342706Z",
    "startEvent": "BRStart",
    "ended": "2024-08-01T11:17:50.3604982Z",
    "endEvent": "BREnd"
}
{{< /expandableCode >}}


{{< expandableCode title="Eksempel på respons som feiler" lang="json" >}}
{
    "title": "Validation failed for task",
    "status": 409,
    "detail": "2 validation errors found for task TaskBekreftelse",
    "validationIssues": [
        {
            "severity": 1,
            "dataElementId": null,
            "field": "regelUtfall",
            "code": "Det er angitt et indirekte grunnlag for reell rettighetshaver, men det er ikke angitt noen mellomliggende virksomheter",
            "description": "Det er angitt et indirekte grunnlag for reell rettighetshaver, men det er ikke angitt noen mellomliggende virksomheter",
            "source": "Altinn.App.AppLogic.Validation.TaskBekreftelseValidator-TaskBekreftelse",
            "customTextKey": "Det er angitt et indirekte grunnlag for reell rettighetshaver, men det er ikke angitt noen mellomliggende virksomheter",
            "customTextParams": null
        },
        {
            "severity": 1,
            "dataElementId": null,
            "field": "regelUtfall",
            "code": "Det er kun angitt en eierposisjon med et ugyldig eierskapsintervall",
            "description": "Det er kun angitt en eierposisjon med et ugyldig eierskapsintervall",
            "source": "Altinn.App.AppLogic.Validation.TaskBekreftelseValidator-TaskBekreftelse",
            "customTextKey": "Det er kun angitt en eierposisjon med et ugyldig eierskapsintervall",
            "customTextParams": null
        }
    ]
}
{{< /expandableCode >}}


Du har nå sendt inn skjemaet til Brønnøysundregistrene!
