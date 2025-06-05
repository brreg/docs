---
title: Beskrivelse av felter
description: Tekstlig beskrivelse av feltene i JSON-skjemaet
weight: 4
---


Denne siden gir en komplett beskrivelse av feltene du finner i [JSON-skjema](https://schema.brreg.no/reelle/altinn/schema.json) for maskinell innrapportering. Tilhørende kodeliste finnes her i [denne Excel-filen](Kodeverk%20MINN.xlsx) 

## Feltbeskrivelse

{{< table class="spesial-tabell" >}}
  <thead>
    <tr>
      <th>Property</th>
      <th>Sub-property</th>
      <th>Beskrivelse</th>
      <th>Kan endres?</th>
      <th>Påkrevd</th>
      <th>Betingelser ved utfylling</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>JSON-schema rotnivå</strong></td>
      <td></td>
      <td>Feltene på rotnivå blir preutfylt automatisk, og skal aldri endres av fagsystem</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>versjon</td>
      <td>Indikerer versjon på skjemaet som skal sendes inn fra fagsystemet</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>endret</td>
      <td>Indikerer dato for når denne versjonen av skjemaet ble produksjonssatt i Altinn</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td><strong>skjemainnhold.metadata</strong></td>
      <td></td>
      <td>Alle feltene under metadata blir preutfylt automatisk, og skal aldri endres av fagsystem</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>tjeneste</td>
      <td>Indikerer hvilket skjema det er</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>tjenestehandling</td>
      <td>Indikerer hvilken type registrering det er snakk om, f.eks. "nyregistrering" eller "endring"</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>rettighetsinformasjonsid</td>
      <td>Unik identifikator som identifiserer rettighetsinformasjon i register over reelle rettighetshavere</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>registreringsid</td>
      <td>Unik identifikator for en bestemt registrering av reelle rettighetshavere</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td><strong>skjemainnhold.fagsystem</strong></td>
      <td></td>
      <td>Alle feltene under fagsystem blir satt automatisk ved innsending. Dvs at fagsystemet ikke skal sette dette selv</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>organisasjonsnummer</td>
      <td>Organisasjonsnummer for fagsystemleverandør</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>navn</td>
      <td>Navn for fagsystemleverandør</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td><strong>skjemainnhold.skjemadata</strong></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>registreringspliktigVirksomhet.organisasjonsnummer</td>
      <td>Organisasjonsnummer for den registreringspliktige virksomheten. Dette vil være den virksomheten som sluttbruker rapporterer for. Feltet blir preutfylt automatisk, og skal aldri endres av fagsystem</td>
      <td>Nei</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>reelleRettighetshavereidentifikasjon</td>
      <td>Kodeverdi (fra kodelista reelleRettighetshavereidentifikasjon) som angir om virksomheten har / kan identifisere reelle rettighetshavere. Angi en av 3 følgende verdier:<br><br>
          1. Har reelle rettighetshavere: reelleRettighetshavereidentifikasjon.harReelleRettighetshavere<br>
          2. Har reelle rettighetshavere, men ingen av disse kan identifiseres: reelleRettighetshavereidentifikasjon.ingenReelleRettighetshavereKanIdentifiseres<br>  
          3. Har ikke reelle rettighetshavere: reelleRettighetshavereidentifikasjon.harIkkeReelleRettighetshavere
      </td>
      <td>Ja</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>aarsakTilAtVirksomhetenIkkeHarReelleRettighetshavere.erEidEllerKontrollertAvOffentligVirksomhet</td>
      <td>Boolsk verdi som angir om årsaken til at virksomheten ikke har reelle rettighetshavere er at den er kontrollert av en offentlig myndighet</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Må angis hvis reelleRettighetshavereidentifikasjon er satt til: "reelleRettighetshavereidentifikasjon.harIkkeReelleRettighetshavere"</td>
    </tr>
    <tr>
      <td></td>
      <td>aarsakTilAtVirksomhetenIkkeHarReelleRettighetshavere.erOffentligVirksomhetUtenlandsk</td>
      <td>Boolsk verdi som angir om den offentlige virksomheten er en utenlandsk virksomhet</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Må angis hvis man har svart true på erEidEllerKontrollertAvOffentligVirksomhet</td>
    </tr>
    <tr>
      <td></td>
      <td>finnesDetReelleRettighetshavereITilleggTilRolleinnehavereForStiftelse</td>
      <td>Boolsk verdi som angir om stiftelsen har reelle rettighetshavere i tillegg til rolleinnehaverne som fra før er registrert i Foretaksregisteret</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis kun hvis registreringspliktig virksomhet er en stiftelse (organisasjonsform STI)</td>
    </tr>
    <tr>
      <td></td>
      <td>reellRettighetshaver (se detaljert feltbeskrivelse for property: reellRettighetshaver nedenfor)</td>
      <td>Array som kan inneholde 0..* reelle rettighetshavere. Reell rettighetshaver er en fysisk person som i siste instans eier eller kontrollerer en registreringspliktig virksomhet</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Må legge inn 1..* reelle rettighetshavere hvis reelleRettighetshavereidentifikasjon er satt til: "reelleRettighetshavereidentifikasjon.harReelleRettighetshavere"</td>
    </tr>
    <tr>
      <td></td>
      <td>kanIkkeIdentifisereFlereReelleRettighetshavere</td>
      <td>Boolsk verdi som angir om virksomheten har kjente reelle rettighetshavere, men også har en eller flere som ikke kan identifiseres</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Må angis hvis reelleRettighetshavereidentifikasjon er satt til: "reelleRettighetshavereidentifikasjon.harReelleRettighetshavere"</td>
    </tr>
    <tr>
      <td></td>
      <td>erVirksomhetRegistrertPaaRegulertMarked</td>
      <td>Boolsk verdi som angir om virksomhet er registrert på et regulert marked (børs)</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis kun hvis registreringspliktig virksomhet har organisasjonsform allmennaksjeselskap (ASA), europeisk selskap (SE) eller sparebank (SPA)</td>
    </tr>
    <tr>
      <td></td>
      <td>regulertMarked.markedstype</td>
      <td>Kodeverdi (fra kodelista markedstype) som angir hvilket marked virksomheten er registrert på</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis kun hvis man først har svart true på erVirksomhetRegistrertPaaRegulertMarked</td>
    </tr>
    <tr>
      <td></td>
      <td>erReelleRettighetshavereRegistrertIUtenlandskRegister</td>
      <td>Boolsk verdi som angir om en norsk avdeling av et utenlandsk foretak (organisasjonsform: NUF) er registrert i et utenlandsk register over reelle rettighetshavere</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis kun hvis registreringspliktig virksomhet har organisasjonsform norsk avdeling av et utenlandsk foretak (NUF)</td>
    </tr>
    <tr>
      <td></td>
      <td>utenlandskRegister.registertype</td>
      <td>Kodeverdi (fra kodelista registertype) som angir hvilket utenlandsk register en norsk avdeling av et utenlandsk foretak (organisasjonsform: NUF) er registrert i</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis kun hvis registreringspliktig virksomhet har organisasjonsform norsk avdeling av et utenlandsk foretak (NUF)</td>
    </tr>
    <tr>
      <td></td>
      <td>rolleinnehaver</td>
      <td>Liste over rolleinnehavere som er registrert på virksomheten i Enhetsregisteret</td>
      <td>Nei</td>
      <td>Betinget</td>
      <td>Hvis registreringspliktig virksomhet har organisasjonsformen stiftelse (STI) vil eksisterende rolleinnehavere i Enhetsregisteret automatisk være reelle rettighetshavere. Disse vil hentes inn og fylles ut automatisk. Fagsystemet trenger ikke sette dette selv</td>
    </tr>
    <tr>
      <td><strong>Sub-property: reellRettighetshaver</strong></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>erRegistrertIFolkeregisteret</td>
      <td>Boolsk verdi som angir om den reelle rettighetshaveren er en person som er registrert i folkeregisteret</td>
      <td>Ja</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>folkeregistrertPerson.foedselsEllerDNummer</td>
      <td>Fødsels- eller D-nummer for person registrert i folkeregisteret</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har svar true på erRegistrertIFolkeregisteret</td>
    </tr>
    <tr>
      <td></td>
      <td>utenlandskPerson.foedselsdato</td>
      <td>Fødselsdato for utenlandsk person</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har svart false på erRegistrertIFolkeregisteret</td>
    </tr>
    <tr>
      <td></td>
      <td>utenlandskPerson.fulltNavn</td>
      <td>Fullt navn for utenlandsk person</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har svart false på erRegistrertIFolkeregisteret</td>
    </tr>
    <tr>
      <td></td>
      <td>utenlandskPerson.bostedsland</td>
      <td>Bostedsland for utenlandsk person (landkode på ISO 3166-1 alpha-3 format)</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har svart false på erRegistrertIFolkeregisteret</td>
    </tr>
    <tr>
      <td></td>
      <td>utenlandskPerson.statsborgerskap</td>
      <td>Statsborgerskap for utenlandsk person (landkode(r) på ISO 3166-1 alpha-3 format). Dette er en string array der man kan legge inn flere statsborgerskap hvis det er snakk om at personen har flere statsborgerskap (eksempel: AUT,SWE)</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har svart false på erRegistrertIFolkeregisteret</td>
    </tr>
    <tr>
      <td></td>
      <td>harPosisjonEierskap</td>
      <td>Boolsk verdi som angir om reell rettighetshaver innehar posisjon eierskap</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Kan kombineres med "harPosisjonKontrollOverStemmerettigheter"</td>
    </tr>
    <tr>
      <td></td>
      <td>posisjonEierskap (se detaljert feltbeskrivelse for property: posisjonEierskap/posisjonKontrollOverStemmerettigheter nedenfor)</td>
      <td>Type kontroll eller eierskap den reelle rettighetshaveren utøver overfor den registreringspliktige virksomheten i siste instans</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Må angis hvis harPosisjonEierskap er satt til true</td>
    </tr>
    <tr>
      <td></td>
      <td>harPosisjonKontrollOverStemmerettigheter</td>
      <td>Boolsk verdi som angir om reell rettighetshaver innehar posisjon kontroll over stemmerettigheter</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Kan kombineres med "harPosisjonEierskap"</td>
    </tr>
    <tr>
      <td></td>
      <td>posisjonKontrollOverStemmerettigheter (se detaljert feltbeskrivelse for property: posisjonEierskap/posisjonKontrollOverStemmerettigheter nedenfor)</td>
      <td>Type kontroll eller eierskap den reelle rettighetshaveren utøver overfor den registreringspliktige virksomheten i siste instans</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Må angis hvis harPosisjonKontrollOverStemmerettigheter er satt til true</td>
    </tr>
    <tr>
      <td></td>
      <td>harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene</td>
      <td>Boolsk verdi som angir om reell rettighetshaver innehar posisjon rett til å utpeke eller avsette minst halvparten av styremedlemmene</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Kan IKKE kombineres med andre posisjoner. Hvis denne settes til true må de andre settes til false</td>
    </tr>
    <tr>
      <td></td>
      <td>grunnlagForPosisjonenRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene</td>
      <td>Kodeverdi (fra kodelista grunnlagstype) som angir grunnlag for posisjonen til den reelle rettighetshaveren. Når den skal settes skal den alltid ha verdien: grunnlagstype.enighetEllerAvtale</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>MÅ angis hvis reell rettighetshaver har posisjon "harPosisjonRettTilAaUtpekeEllerAvsetteMinstHalvpartenAvStyremedlemmene"</td>
    </tr>
    <tr>
      <td></td>
      <td>harPosisjonKontrollPaaAnnenMaate</td>
      <td>Boolsk verdi som angir om reell rettighetshaver innehar posisjon kontroll på annen måte</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Kan IKKE kombineres med andre posisjoner. Hvis denne settes til true må de andre settes til false</td>
    </tr>
    <tr>
      <td></td>
      <td>beskrivelseAvPosisjonenKontrollPaaAnnenMaate</td>
      <td>Fritekst som beskriver hva som gjør at den reelle rettighetshaveren har posisjonen kontroll på annen måte</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>MÅ angis hvis reell rettighetshaver har posisjon "harPosisjonKontrollPaaAnnenMaate"</td>
    </tr>
    <tr>
      <td></td>
      <td>harPosisjonAvgittGrunnkapital</td>
      <td>Boolsk verdi som angir om reell rettighetshaver innehar posisjon avgitt grunnkapital</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Denne kan bare settes til true hvis virksomheten har organisasjonsform stiftelse (STI). I alle andre sammenhenger skal den ha verdien false</td>
    </tr>
    <tr>
      <td></td>
      <td>harPosisjonRettTilAaUtpekeEtFlertallAvStyremedlemmene</td>
      <td>Boolsk verdi som angir om reell rettighetshaver innehar posisjon rett til å utpeke et flertall av styremedlemmene</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Denne kan bare settes til true hvis virksomheten har organisasjonsform stiftelse (STI). I alle andre sammenhenger skal den ha verdien false</td>
    </tr>
    <tr>
      <td></td>
      <td>harPosisjonDestinatar</td>
      <td>Boolsk verdi som angir om reell rettighetshaver innehar posisjon destinatar</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Denne kan bare settes til true hvis virksomheten har organisasjonsform stiftelse (STI). I alle andre sammenhenger skal den ha verdien false</td>
    </tr>
    <tr>
      <td></td>
      <td>harPosisjonSaerligeRettigheter</td>
      <td>Boolsk verdi som angir om reell rettighetshaver særlige rettigheter</td>
      <td>Ja</td>
      <td>Ja</td>
      <td>Denne kan bare settes til true hvis virksomheten har organisasjonsform stiftelse (STI). I alle andre sammenhenger skal den ha verdien false</td>
    </tr>
    <tr>
      <td><strong>Sub-property: posisjonEierskap / posisjonKontrollOverStemmerettigheter</strong></td>
      <td></td>
      <td>Type kontroll eller eierskap den reelle rettighetshaveren utøver overfor den registreringspliktige virksomheten i siste instans</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>stoerrelsesintervall</td>
      <td>Kodeverdi (fra kodelista stoerrelsesintervall) som angir hvor stor prosentandel reell rettighetshaver har av posisjon "eierskap" eller posisjon "kontroll over stemmerettigheter"</td>
      <td>Ja</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>grunnlag</td>
      <td>Kodeverdi(er) (fra kodelista grunnlagstype) som angir grunnlag for posisjonen til den reelle rettighetshaveren. NB! Det er mulig å angi flere grunnlag for posisjonen i dette feltet. Kodeverdiene separeres med komma (eks: "grunnlagstype.direkte,grunnlagstype.indirekte")</td>
      <td>Ja</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet</td>
      <td>Array som kan inneholde 0..* mellomliggende virksomheter</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis KUN hvis man først har angitt grunnlag "grunnlagstype.indirekte"</td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet.erUtenlandskVirksomhet</td>
      <td>Boolsk verdi som angir om angitt mellomliggende virksomhet er utenlandsk</td>
      <td>Ja</td>
      <td>Ja</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet.norskVirksomhet.organisasjonsnummer</td>
      <td>Organisasjonsnummer for en norsk mellomliggende virksomhet</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har angitt false på erUtenlandskVirksomhet</td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet.utenlandskVirksomhet.registreringsnummerIHjemlandet</td>
      <td>Registreringsnummer i hjemlandet for den utenlandske mellomliggende virksomheten</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har angitt true på erUtenlandskVirksomhet</td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet.utenlandskVirksomhet.navn</td>
      <td>Virksomhetsnavn for den utenlandske mellomliggende virksomheten</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har angitt true på erUtenlandskVirksomhet</td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet.utenlandskVirksomhet.adresse.friAdressetekst1</td>
      <td>Adresselinje for den utenlandske mellomliggende virksomheten</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Angis hvis man har angitt true på erUtenlandskVirksomhet</td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet.utenlandskVirksomhet.adresse.friAdressetekst2</td>
      <td>Adresselinje for den utenlandske mellomliggende virksomheten</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Kan angis hvis man har angitt true på erUtenlandskVirksomhet</td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet.utenlandskVirksomhet.adresse.friAdressetekst3</td>
      <td>Adresselinje for den utenlandske mellomliggende virksomheten</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Kan angis hvis man har angitt true på erUtenlandskVirksomhet</td>
    </tr>
    <tr>
      <td></td>
      <td>mellomliggendeVirksomhet.utenlandskVirksomhet.adresse.landkode</td>
      <td>Landkode til hjemlandet for den utenlandske mellomliggende virksomheten (ISO 3166-1 alpha-2 format)</td>
      <td>Ja</td>
      <td>Betinget</td>
      <td>Kan angis hvis man har angitt true på erUtenlandskVirksomhet</td>
    </tr>
  </tbody>
{{< /table >}}