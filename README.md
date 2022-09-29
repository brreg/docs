# Brønnøysundregistrene dokumentasjon

Vi er i gang med å forbedre [Brønnøysundregistrenes dokumentasjon](https://brreg.github.io/docs/) og gjøre den enkel å vedlikeholde.

# Getting started

- Skaff tilgang til en github bruker tilkoblet din brsys-mail og clone deretter dette docs-repoet
- Last ned hugo, se her for instruksjoner: [Nedlasting av Hugo](https://gohugo.io/getting-started/installing/). Filer for nedlasting er tilgjengelige på [Hugos releases GitHub](https://github.com/gohugoio/hugo/releases). Om du bruker vanlig Windows så kan du velge releasen med navn som slutter på `windows-amd64.zip`.
- Pakk ut filen og legg den i rotmappen på docs-repoet. Ved innsjekk av endringer vil git overse Hugo-filen (.gitignore) slik at den ikke lastes opp.

## Ønsker du å bidra?

1. Pull eksisterende endringer.
2. Gjør endringene du ønsker på din lokale kopi, helst direkte på `master` branch.
3. Inspiser at resultatet er slik du ønsker, f.eks vha `hugo server`. Dette starter en lokal webserver som kan nås via default adresse [localhost:1313/docs](localhost:1313/docs). Merk at `hugo` kan være sperret av gruppepolicy, og da må kan man måtte bruke kommandolinje startet med administratortilgang for å kjøre programmet.
4. Deploy endringene ved å committe endringer og pushe til `master`



Du kan også foreslå forbedringer eller påpeke bugs ved å [opprette en issue](https://github.com/brreg/docs/issues).

## Oppsettet av dokumentasjonsrepoet

Hugo genererer med kommandoen `hugo` et sett med statiske dokumentasjonsfiler i mappen `public`. 
Ved pushing til `master` vil en GitHub Workflow automatisk kjøre `hugo` og legge genererte html-filer i branchen `gh-pages`. Oppdaterte html-filer blir automatisk tilgjengelige i løpet av få strakser på [BRDocs](https://brreg.github.io/docs/), vår GitHub Site for dokumentasjon. På github finnes det under [Deployments](https://github.com/brreg/docs/deployments) automatisk deploy av endringer pushet til [gh-pages](https://docs.github.com/en/github/working-with-github-pages/getting-started-with-github-pages).
