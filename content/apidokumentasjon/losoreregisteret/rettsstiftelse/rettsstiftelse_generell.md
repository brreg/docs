---
title: Generelt - Uthenting av rettsstiftelser
description: Beskrivelser av API innen domene Rettsstiftelse
weight: 110
---

## Innledning

Brønnøysundregistrene tilbyr en begrenset, standardisert maskin-til-maskin-tjeneste (API) som kan benyttes av eksterne partnere for innsyn i rettsstiftelser fra Løsøregisteret.

Denne dokumentasjonen viser hvordan eksterne systemer kan integrere seg mot APIet, og hvordan man benytter seg av tjenesten for å hente data.

Det er også blitt opprettet en referanseapplikasjon for å gjøre det enklere å se hvordan man skal integrere.
Koden for denne er lagt ut i brreg sitt repository på github: [refapp-integrasjon](https://github.com/brreg/refapp-integrasjon)

## Syntetiske testdata

For enkelte fødsels-, organisasjons og registreringsnummer kan det være registrert flere tusen rettsstiftelser i vårt testmiljø. 
Ved oppslag på disse kan du oppleve time-out feilmelding. Forsøk da oppslag på en annen identifikator. 
Brønnøysundregistrene benytter selv det samme testmiljøet, og testdataene er ikke statisk. 
Disse endres kontinuerlig basert på vår egen testing, samt tinglysning i vårt testmiljø som utføres av eksterne brukere. 
Du vil også sporadisk kunne finne testdata som har innhold som ikke er i henhold til forretningsregler, eller testdata som er mangelfulle.

## API-referanse

Denne tjenesten tilbyr opplysninger om:

* Rettsstiftelser tilknyttet kjøretøy gitt kjøretøyets registreringsnummer (Merk at oppslag på personlig kjennemerke ikke er støttet)
* Rettsstiftelser tilknyttet organisasjon gitt tilhørende organisasjonsnummer
* Rettsstiftelser tilknyttet person gitt personens fødselsnummer eller d-nummer
* Totalbestand, alle aktive rettsstiftelser.
* Endringslogg, endringer på rettsstiftelser opp til og med 30 dager tilbake.

Dokumentasjon er også tilgjengelig i Swagger:

* [Testmiljø](https://losoreregisteret.ppe.brreg.no/registerinfo/swagger-ui.html)
* [Produksjonsmiljø](https://losoreregisteret.brreg.no/registerinfo/swagger-ui.html)

Eksempel på request- og response-objekter (implementert i Java) for APIet kan sees her: [refapp-integrasjon DTOer](https://github.com/brreg/refapp-integrasjon/tree/main/src/main/java/refappintegrasjon/dto)

Klokkeslettprioritet ble innført i Løsøreregisteret fra 1. mars 2024. Før denne dato gjelder dagsprioritet.
Tidsangivelse for innkomsttidspunkt vil være tt:mm.00. Sekunder og evt. ms angis med verdi 0.

## Sikkerhetsmekanismer

Siden dette er begrensede API så skal kallende parter autentiseres gjennom [Maskinporten](https://docs.digdir.no/maskinporten_guide_apikonsument.html).

For å kunne få tilgang til våre begrensede API er det tre forutsetninger:

1. Virksomhetssertifikat
2. Registrert klient hos Maskinporten.
3. JWT-token fra Maskinporten mot scopet `brreg:losore/tlg`

Tokenet som hentes fra Maskinporten må bli sendt som autorisasjonstoken (Bearer token) når et kall mot Løsøreregisteret blir utført.

Se [veiledning for integrasjon mot Maskinporten]({{<ref "mp-integrasjonsveiledning.md">}}).

[Regelverk](https://lovdata.no/dokument/SF/forskrift/2015-12-11-1668/%C2%A76): Hjemler for tilgjengeliggjøring av data fra Brønnøysundregistrene.

## HTTP-statuskoder

Oversikt over HTTP-statuskoder i APIet.

| HTTP-kode                 | Beskrivelse |
|:------------------------- |:----------- |
| 200 OK                    | Henting av data gikk bra |
| 400 Bad Request           | Feil i spørring. Applikasjonen vil gi en detaljert feilmelding for hva som er feil med spørring |
| 403 Forbidden             | Feil ved autentisering eller autorisering. Bearer tokenet som ble sendt inn er ikke gyldig eller har ikke en gyldig avtale om maskinelt oppslag på opplysninger i Løsøreregisteret |
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
| orgnr | Identifikasjonsnummer for virksomhet |
| regnr | Registreringsnummer knyttet til et kjøretøy / tilhenger |
| fnr | Fødselsnummer for person |
| d-nummer | Identifikasjonsnummer som tildeles personer med midlertidig tilknytning til Norge, det vil si som ikke er bosatt i Norge. Består av en modifisert sekssifret fødselsdato og et femsifret personnummer. Fødselsdatoen modifiseres ved at det legges til 4 på det første sifferet. |
| rettsstiftelse | Bestemmelse i et dokument som stifter, forandrer, overdrar, behefter, anerkjenner eller opphever en rettighet |

---
