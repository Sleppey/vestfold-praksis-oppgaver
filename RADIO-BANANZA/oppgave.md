# Oppgave: Hva spilles på P3 Musikk?

## Bakgrunn

Jørgen lurer ofte på hvilken låt og artist som spilles akkurat nå på **P3 Musikk**. I stedet for å sjekke [radio.nrk.no/direkte/p3musikk](https://radio.nrk.no/direkte/p3musikk) manuelt, skal du lage en enkel nettside som viser dette automatisk – og som oppdaterer seg selv når låten byttes.

## Mål

Når du er ferdig skal Jørgen kunne åpne nettsiden (f.eks. via en lokal utviklingsserver) og se:

- Hvilken **låt** som spilles akkurat nå
- Hvilken **artist** som spilles
- Informasjonen skal **oppdatere seg selv** når NRK bytter til neste låt (du velger selv hvordan – f.eks. med jevne mellomrom, eller når du oppdager at noe har endret seg)

## Rammer for løsningen

- **Bruk Svelte.** Hovedpoenget med oppgaven er å bli kjent med Svelte som rammeverk. Start gjerne med den offisielle opplæringen på [svelte.dev/tutorial](https://svelte.dev/tutorial) før du setter i gang.
- **TypeScript anbefales, men er valgfritt.** Vi vil gjerne at du prøver TypeScript, siden det er mye brukt i arbeidslivet. Føles det som for mye på én gang, kan du skrive i vanlig JavaScript i stedet – og eventuelt gå over til TypeScript senere i oppgaven.
- Sett opp prosjektet med [SvelteKit](https://svelte.dev/docs/kit) (eller et annet standard Svelte-oppsett du finner naturlig), som en SPA. Du trenger ikke servere noe fra en backend for denne oppgaven.
- **Ingen eksterne pakker/biblioteker** utover Svelte/SvelteKit-oppsettet, med mindre det er helt nødvendig for å løse oppgaven. Kan du løse det med innebygde nettleser-API-er (f.eks. `fetch`), skal du gjøre det.
- Del opp logikken i egne moduler/filer der det gir mening (f.eks. én modul for å hente data fra NRK-API-et, og én komponent for visning).
- **Bruker du TypeScript:** skriv koden i `.ts`-filer og typede `.svelte`-komponenter (`<script lang="ts">`), og definer **typer/interfaces** for dataene du henter fra API-et i stedet for å bruke `any`.
- **Skriv koden selv, uten KI.** Bruk dokumentasjon på nettet (f.eks. [svelte.dev](https://svelte.dev/docs), [MDN](https://developer.mozilla.org/) og [TypeScript-håndboka](https://www.typescriptlang.org/docs/handbook/)) når du står fast. Ikke kopier kode direkte fra andre kilder – skriv den sjæl. Spør oss gjerne hvis du blir sittende fast!
- Design/utseende står du fritt til å velge selv. Hold det gjerne enkelt til å begynne med – funksjonalitet er viktigere enn utseende i denne omgangen.

## Fremgangsmåte – finne API-et

NRK har ikke et offentlig dokumentert API du bare kan slå opp, men siden radio.nrk.no/direkte/p3musikk viser denne informasjonen i nettleseren, må dataene hentes fra et sted. Slik kan du finne det:

1. Åpne [radio.nrk.no/direkte/p3musikk](https://radio.nrk.no/direkte/p3musikk) i nettleseren.
2. Åpne **utviklerverktøyene** (F12 eller høyreklikk → Inspiser).
3. Gå til fanen **Network** (Nettverk).
4. Filtrer gjerne på **Fetch/XHR** for å slippe unna bilder, CSS osv.
5. Last siden på nytt (F5) og se etter forespørsler som returnerer JSON-data med informasjon om låt/artist/program.
6. Klikk på en aktuell forespørsel og se på:
   - **URL-en** (dette er endepunktet du skal bruke)
   - **Response**-fanen (dette er dataformatet du må lese i koden din)
7. Test gjerne endepunktet direkte i nettleseren eller med et verktøy som `curl`/Postman, for å bli kjent med strukturen på svaret før du begynner å kode.

**Tips:**
- Se etter ord som `playback`, `metadata`, `channel`, `playlist` eller lignende i URL-ene.
- Noen NRK-API-er kan ha begrensninger på hvilke domener som får kalle dem (CORS). Dukker det opp feilmeldinger om dette i konsollen, er det noe å undersøke og spørre om – ikke noe å gi opp på.
- Dataene kan være strukturert med informasjon om "nå-spilles" og gjerne også "forrige/neste". Utforsk responsen grundig.

## Delmål / foreslått rekkefølge

1. **Sett opp et Svelte-prosjekt** (f.eks. med SvelteKit). Velg TypeScript eller JavaScript når du oppretter prosjektet.
2. **Finn endepunktet** ved hjelp av Network-fanen, slik som beskrevet over.
3. **Bli kjent med dataene** du får tilbake fra API-et (låtnavn, artist, ev. mer). Bruker du TypeScript, definerer du typer for dem her.
4. **Hent data med `fetch`** i en egen modul, og skriv resultatet til konsollen (`console.log`) for å bekrefte at du får riktige data.
5. **Vis data i en Svelte-komponent** – bruk Sveltes reaktivitet (f.eks. `$state` i Svelte 5) til å vise låtnavn og artist i stedet for å bare logge til konsollen.
6. **Style siden** litt med CSS, slik at det ser noenlunde presentabelt ut.
7. **Få siden til å oppdatere seg selv**, f.eks. ved å hente nye data med jevne mellomrom (`setInterval`) og oppdatere visningen kun når noe faktisk har endret seg.
8. **Rydd opp i koden**: fornuftig mappestruktur, gode variabelnavn, logikk delt inn i komponenter/moduler etter ansvar (f.eks. én modul for å hente data, én komponent for visning).

## Git og arbeidsflyt

I denne oppgaven skal du jobbe slik man ofte gjør i et utviklingsteam: med branches, pull requests (PR) og code review.

**Oppsett**
- Det første oppsettet av prosjektet kan du committe rett til `main`. Etter det skal du ikke committe direkte til `main`.
- Legg til en `.gitignore` om det er relevant (SvelteKit lager som regel en for deg – sjekk hva som står i den).

**Slik jobber du med hvert delmål**
1. Sørg for at du står på en oppdatert `main` (`git switch main` og `git pull`).
2. Lag en ny branch med et beskrivende navn, f.eks. `hent-data` eller `auto-oppdatering`.
3. Gjør committer underveis i naturlige steg. Skriv korte, beskrivende commit-meldinger som forklarer *hva* som er gjort og gjerne *hvorfor*.
4. Push branchen og opprett en **pull request** mot `main`. Beskriv i PR-en hva du har gjort, hvorfor, og hvordan man kan teste det.
5. Be veilederen din om **review**, og **vent på godkjenning** før du merger. Ikke merge din egen PR uten godkjenning.
6. Får du kommentarer, retter du opp med nye committer på samme branch og svarer på kommentarene i PR-en. Er du uenig i en kommentar, er det lov å si det og forklare hvorfor.
7. Når PR-en er godkjent og merget: bytt tilbake til `main`, hent ned endringene med `git pull`, og slett den gamle branchen.

**Mens du venter på review** kan du godt begynne på neste delmål i en ny branch fra `main`. Bygger neste steg på kode som ikke er merget ennå, kan du spørre veilederen din hvordan du bør løse det.

Les gjerne GitHubs egen dokumentasjon om [pull requests](https://docs.github.com/en/pull-requests) før du starter.

## Læringsmål

- Bli kjent med **Svelte** som rammeverk – komponenter, reaktivitet og hvordan en Svelte-app er bygd opp
- Forstå og bruke **`fetch`** til å hente data fra et eksternt API
- Lese og tolke **JSON**-responser
- Jobbe med **moduler** (`import`/`export`) og komponent-basert struktur
- Bruke **utviklerverktøy** i nettleseren til å utforske nettverkstrafikk
- Praktisk bruk av **Git**: committe i fornuftige steg med gode meldinger
- *(Hvis du velger TypeScript)* Grunnleggende **TypeScript**: typer, interfaces, og å type data fra et eksternt API

## Definition of done

- [ ] Siden viser låt og artist som spilles nå på P3 Musikk
- [ ] Informasjonen oppdateres automatisk uten at man må laste siden på nytt manuelt
- [ ] Prosjektet er satt opp med Svelte
- [ ] *(Hvis TypeScript)* Dataene fra API-et er typet (ikke `any`)
- [ ] Logikk og visning er delt inn i moduler/komponenter etter ansvar
- [ ] Ingen unødvendige eksterne pakker er brukt
- [ ] Koden er skrevet av deg selv, med hjelp fra dokumentasjon – ikke KI
- [ ] Prosjektet ligger i et git-repo med flere, meningsfulle commits

## Videre arbeid (senere)

Dette er en start – vi kan bygge videre og gjøre prosjektet mer avansert etter hvert. Ikke bekymre deg for å "fremtidssikre" koden for mye ennå; fokuser på å få noe som fungerer, og gjør det ryddig underveis.

Lykke til! 🎧