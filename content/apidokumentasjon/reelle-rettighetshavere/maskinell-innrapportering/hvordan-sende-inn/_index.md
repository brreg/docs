---
title: Innsending av Altinn-skjema
description: Beskrivelse av hvordan man sender inn registreringer som tredjeleverandør.
weight: 100
---

Som sluttbrukersystem kan du sende inn opplysninger om Reelle rettighetshavere til oss ved å følge stegene på denne siden:
<!-- TOC -->
  * [Sekvensdiagram](#sekvensdiagram)
  * [ID-porten](#id-porten)
    * [1. Sende sluttbruker til ID-porten](#1-sende-sluttbruker-til-id-porten)
  * [Veksle inn Altinn-token](#veksle-inn-altinn-token)
    * [2. Veksle inn ID-porten-tokenet til et Altinn-token](#2-veksle-inn-id-porten-tokenet-til-et-altinn-token)
  * [API-kall mot Altinn APP](#api-kall-mot-altinn-app)
    * [3. Hent partyId til virksomheten](#3-hent-partyid-til-virksomheten)
    * [4. Hent preutfylte skjemadata](#4-hent-preutfylte-skjemadata)
    * [5. Du bygger opp opplysninger om Reelle rettighetshavere som JSON i ditt system](#5-du-bygger-opp-opplysninger-om-reelle-rettighetshavere-som-json-i-ditt-system)
    * [6. Opprett en instans av vårt Altinn-skjema](#6-opprett-en-instans-av-vårt-altinn-skjema)
    * [7. Du setter opplysninger om Reelle rettighetshavere som skjemadata på instansen (som du bygget opp i steg 5.)](#7-du-setter-opplysninger-om-reelle-rettighetshavere-som-skjemadata-på-instansen-som-du-bygget-opp-i-steg-5)
    * [8. Du går videre til neste prosess (Validering av skjema)](#8-du-går-videre-til-neste-prosess-validering-av-skjema)
    * [9. Du sender inn skjemaet til Brønnøysundregistrene](#9-du-sender-inn-skjemaet-til-brønnøysundregistrene)
<!-- TOC -->


## Sekvensdiagram

![Sekvensdiagram](sekvensdiagram_minn.png)

## ID-porten

### 1. Sende sluttbruker til ID-porten

For at ditt system skal få lov til å sende inn registrering av reelle rettighetshavere inn til oss må din sluttbruker
autentisere seg gjennom ID-porten.
Vi anbefaler at du
følger [Digdirs integrasjonsguide for autentisering i ID-porten](https://docs.digdir.no/docs/idporten/oidc/oidc_guide_idporten.html).

Når du følger guiden må du gjøre følgende steg:

1. Sende en autentiseringsforespørsel til autorisasjons-endepunktet
    * **Her må du også legge til et query-param `scope` med verdi `altinn:instances.write`**. Denne trenger du for å få
      lov til å gjøre CRUD-forespørsler mot Altinns APP API.
2. Bruker autentiserer seg på sin foretrukkende måte, feks BankId. Sluttbruker må også godkjenne at ditt
   sluttbrukersystem får tilgang scope `altinn:instances.write` på vegne at sluttbruker.
3. Bruker blir redirected tilbake til din tjeneste
4. Du kaller token-endepunktet og utsteder et ID-porten-token.

{{< expandableCode title="Eksempel på et B64-encoded ID-porten-token" lang="text">}}
eyJraWQiOiJkaWdpdGFsaXNlcmluZ3NkaXJla3RvcmF0ZXQtLWNlcnQwIiwiYWxnIjoiUlMyNTYifQ.eyJzdWIiOiIxOTg1NTQ5NzkyNCIsImFjciI6ImlkcG9ydGVuLWxvYS1zdWJzdGFudGlhbCIsInNjb3BlIjoiYWx0aW5uOmluc3RhbmNlcy53cml0ZSIsImlzcyI6Imh0dHBzOi8vdGVzdC5pZHBvcnRlbi5ubyIsImNsaWVudF9hbXIiOiJjbGllbnRfc2VjcmV0X3Bvc3QiLCJwaWQiOiIxOTg1NTQ5NzkyNCIsImV4cCI6MTcxODEwMzY4MywiaWF0IjoxNzE4MTAzMDgzLCJqdGkiOiIyMEszRHVaSWRrQSIsImNsaWVudF9pZCI6Ijk3YWMzMjg2LTU3ZWQtNDMzMy05ODU5LTdkMGE4NTIzZTdmZiIsImNvbnN1bWVyIjp7ImF1dGhvcml0eSI6ImlzbzY1MjMtYWN0b3JpZC11cGlzIiwiSUQiOiIwMTkyOjk3NDc2MDY3MyJ9fQ.Lvi--jq2GuM3VEb3K8aFFJZqzqSewHMmHqap6eV7Bibl3nZ9dTWTUhrkNIr4ZSHZkBvIk-A6DcnF8L47rvJVgmN0kczJDVXCv1E8W3yu5mA57k0uvZIxXW0paH6ldQZ2vJL_3iyhg9GLmiU-He5JTtwo_ULo0VX6DVt97lhVf_WHrLY9steIW82ujeMY3m-qUbgRTT9h1LAITpfpX8Mavk1B4gDwzYYx-6S2VNUOMo72b466mAM5-4JUejpPLwCpAr2LNT7pgEh8p8cxHGj0cKNpJ_nqbp7Awc2tJSpYS53YgMIwaYiZA5oKWvVc6RTTx0GgQrHL2IMnK2ObHIBmCPH2vKjwYpZQUBwkXCglxlxdTn9lMmYzA3fLCrQKt_SRDL9GoAjLjgz_h-E0N-hVpBsRJY_K_xgPbqdanhG6pTE352uwuaTVAUpAISRHA-So6yFm2A1Pq-sN5FBpjF6s6KFWmXz3Ro6YXEhWCiuJHkl-GdEnHGq026L3JpNddpmJ
{{< /expandableCode >}}

For å se innholdet til et slikt token kan du B64-decode det, eller bruke verktøy, feks https://jwt.io/.

{{< expandableCode title="Eksempel på et ID-porten-token etter decoding" lang="json" >}}
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

For å veksle inn Altinn-tokenet må du sette følgende headere:

* `ApiKey` Du må legge inn ApiKey-en som du fikk når du bestilte tilgang til Altinns REST-APIer.
* `Authorization`: Her må du legge til ID-porten-tokenet du ustedte fra ID-porten. Siden dette er et Bearer-token skal
  verdien av tokenet være: `Bearer <<idporten access_token>>`

ID-porten-tokenet kan veksles inn ved å kalle Altinns exchange-endepunkt:

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

## API-kall mot Altinn APP

**I alle videre API-kall mot Altinn må du sette følgende headere:**

* `ApiKey` Du må legge inn ApiKey-en som du fikk når du bestilte tilgang til Altinns REST-APIer.
* `Authorization`: Her må du legge til **Altinn-tokenet** vekslet inn. Siden dette er et Bearer-token skal verdien av
  tokenet være: `Bearer <<altinn-token>>`

{{< warning >}}
Husk at du må sette begge disse headerne i alle kallene nedenfor.
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
        "partyId": 51460912,
        "partyUuid": "ec919d0d-4fe6-436b-87d1-b036ba364df8",
        "partyTypeName": 2,
        "orgNumber": "211089172",
        "ssn": null,
        "unitType": "AS",
        "name": "KORREKT ALLMEKTIG TIGER AS",
        "isDeleted": false,
        "onlyHierarchyElementWithNoAccess": false,
        "person": null,
        "organization": null,
        "childParties": [
            {
                "partyId": 51938711,
                "partyUuid": "8764e79c-53d3-4906-92c1-4901829a5026",
                "partyTypeName": 2,
                "orgNumber": "314796748",
                "ssn": null,
                "unitType": "BEDR",
                "name": "KORREKT ALLMEKTIG TIGER AS",
                "isDeleted": false,
                "onlyHierarchyElementWithNoAccess": false,
                "person": null,
                "organization": null,
                "childParties": null
            }
        ]
    },
    {
        "partyId": 50714238,
        "partyUuid": "c4cc127c-d26a-4cd7-a2a0-c1442b44e75d",
        "partyTypeName": 1,
        "orgNumber": "",
        "ssn": "19855497924",
        "unitType": null,
        "name": "TRAGEDIE MINST",
        "isDeleted": false,
        "onlyHierarchyElementWithNoAccess": false,
        "person": null,
        "organization": null,
        "childParties": null
    }
]
{{< /expandableCode >}}

### 4. Hent preutfylte skjemadata

Vi forhåndsutfyller alle skjemainstanser med preutfylte data. Alle skjemainstanser blir preutfylt med:

* rettighetsinformasjonsid
* registreringsid

**Disse feltene og verdiene du henter her _MÅ_ være satt i steget når du setter skjemadataen**

For å forenkle prosessen med å sende inn nye opplysninger om reelle rettighetshavere vil skjemainstansen være preutfylt med forrige innrapporterte data.
Du kan da ta utgangspunkt i den preufylte skjemadataen, gjøre endringer på opplysningene, og sende disse inn.

`GET {{altinn-miljø}}/brg/rrh-innrapportering/prefill/{partyId}`

{{< expandableCode title="Eksempel på prefilldata for en virksomhet som aldri har rapportert inn reelle rettighetshavere" lang="json" >}}
{
    "versjon": "0.0.7",
    "endret": "2024-05-07",
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


{{< expandableCode title="Respons for en virksomhet som har sendt inn registrering fra før" lang="json" >}}
{
  "versjon": "0.0.7",
  "endret": "2024-05-07",
  "skjemainnhold": {
    "metadata": {
      "tjeneste": "rrh.ktr.reelle",
      "tjenestehandling": "endring",
      "rettighetsinformasjonsid": "RRH202300000020",
      "registreringsid": "cace0a64-cf41-4c33-af37-a6f16aa9e356"
    },
    "fagsystem": {
      "organisasjonsnummer": "313496058",
      "navn": "Sluttbrukersystem sitt navn"
    },
    "skjemadata": {
      "registreringspliktigVirksomhet": {
        "organisasjonsnummer": "311780352"
      },
      "reelleRettighetshavereidentifikasjon": "reellerettighetshavereidentifikasjon.harReelleRettighetshavere",
      "reellRettighetshaver": [
        {
          "erRegistrertIFolkeregisteret": true,
          "folkeregistrertPerson": {
            "foedselsEllerDNummer": "05910298382"
          },
          "harPosisjonEierskap": true,
          "posisjonEierskap": {
            "stoerrelsesintervall": "stoerrelsesintervall.intervall3",
            "grunnlag": "grunnlagstype.direkte",
            "mellomliggendeVirksomhet": []
          },
          "harPosisjonKontrollOverStemmerettigheter": false,
          "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene": false,
          "harPosisjonAvgittGrunnkapital": false,
          "harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene": false,
          "harPosisjonDestinatar": false,
          "harPosisjonSaerligeRettigheter": false
        }
      ],
      "kanIkkeIdentifisereFlereReelleRettighetshavere": false,
      "rolleinnehaver": []
    }
  }
}
{{< /expandableCode >}}

### 5. Du bygger opp opplysninger om Reelle rettighetshavere som JSON i ditt system

{{< info >}}
Vi jobber med en side som forklarer hvilke felter som skal settes når. <strong>"Lenke kommer"</strong>.
{{< /info >}}

JSON-skjema for å validere endringer er tilgjengelig her: **"Lenke kommer"**. Sjekk at versjonsnummeret på skjemaet 
samsvarer med feltet `versjon` i de preutfylte skjemadataene ([steg 4.](#4-hent-preutfylte-skjemadata)).

Se gjerne [siden med eksempler](../eksempler-paa-registrering) for å se eksempler på ferdigutfylte JSON-opplysninger. 

For å teste hvordan ulike kombinasjoner av reelle rettighetshavere skal settes, kan du manuelt fylle disse ut i vårt Altinn-skjema på TT02. 
Etterpå kan du maskinelt hente ut preutfylte skjemadata ([steg 4.](#4-hent-preutfylte-skjemadata)), og se hvordan opplysningene ser ut i JSON.

{{< info >}}
<strong>Selv om virksomheten ikke har innrapportert opplysninger om reelle rettighetshavere tidligere, må du alltid ta utgangspunkt i prefilldata når du skal rapportere inn reelle rettighetshavere i ditt sluttbrukersystem!</strong><br> 
Feltene versjon og endret, samt innholdet i "metadata" som du rapporter inn <strong> må være identisk med innholdet du hentet ut i prefilldataen</strong>.
{{< /info >}}

Når du har ferdigstilt opplysningene som JSON kan du gå videre til neste steg.

### 6. Opprett en instans av vårt Altinn-skjema
{{< warning >}}
Hvis det har tatt tid å fylle ut opplysninger kan det hende at Altinn-tokenet har gått ut. Da må du gjenta steg 1. og steg 2., slik at du får et gyldig Altinn-token.
{{< /warning >}}

Med en ferdigstilt registrering kan du sende denne inn til oss.
Første steg er å opprette en instans av vårt Altinn-skjema. Dette gjør du med følgende API-kall:

`POST {{altinn-miljø}}/brg/rrh-innrapportering/instances?instanceOwnerPartyId={{partyId}}`
* Her må du bruke `partyId` som du hentet i steg 3.

I responsen får du UUID `skjema_instans_id` fra feltet `id` og `skjema_instans_data_id` fra feltet `data.id`, som du må bruke i de påfølgende kallene.
Merk at id-feltet inneholder både partyId og skjema_instans_data_id. PartyId må fjernes for å få kun UUID-en.

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


### 7. Du setter opplysninger om Reelle rettighetshavere som skjemadata på instansen (som du bygget opp i steg 5.)

Du må nå sette skjemadata som du opprettet i steg 5 på instansen. Dette gjør du ved å kalle dette endepunktet:
`PUT {{altinn-miljø}}/brg/rrh-innrapportering/instances/{{partyId}}/{{skjema_instans_id}}/data/{{skjema_instans_data_id}}?dataType=Brønnøysundregistrene_ReelleRettighetshavere_M`
* Her må du bruke `skjema_instans_id` og `skjema_instans_data_id` fra forrige API-kall.

### 8. Du går videre til neste prosess (Validering av skjema)

Du kan nå gå videre til neste prosess i Altinn. Dette fører til at skjemadataen du har satt blir validert, og at skjemaet blir klargjort for innsending.
Du kan gå til neste prosess ved å kalle endepunktet:

`PUT {{altinn-miljø}}/brg/rrh-innrapportering/instances/{{party_id}}/{{skjema_instans_id}}/process/next`
* Om skjemaet inneholder feil, vil du få feilmelding.

### 9. Du sender inn skjemaet til Brønnøysundregistrene

Om du ikke fikk noen feilmeldinger i forrige steg, kan du gå til neste prosess, BrEnd, som avslutter instansen.
Dette sender også inn skjemaet inn til oss. Dette gjør du ved å kalle endepunktet:

`PUT {{altinn-miljø}}/brg/rrh-innrapportering/instances/{{party_id}}/{{skjema_instans_id}}/process/next?elementId=BREnd`

Du har nå sendt inn skjemaet til Brønnøysundregistrene!
