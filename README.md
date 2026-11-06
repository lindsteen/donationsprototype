# Donationsapp

Redesign af GivVidere-appen (bestil afhentning af møbler / aflevér selv) i rodekors.dk-stil, plus en admin-side til butikkerne ("backend") i Røde Kors' designsystem (rk-ui-design, platform "anden").

- Original: https://donate-doorstep-delight.lovable.app/
- Prototyper (Claude Design-lærreder):
  - "GivVidere – Bestil afhentning" – donorens webformular, 5 skærme (trin 1–3, kvittering, aflevér selv)
  - "Donationer til genbrug - backend" – admin-siden (tidligere "GivVidere – Admin")
- Live: https://lindsteen.github.io/donationsprototype/ (repo `lindsteen/donationsprototype`). Forsiden samler formular, admin og auto-mails med navigation i toppen; filerne fra `output/` ligger i roden.

## Filer

| Fil | Indhold |
| --- | --- |
| `output/index.html` | Samlet visning med navigation: Webformular, Admin backend og Auto-mails. Bygges med `python byg_samlet.py output`, når en anden fil i `output/` er ændret |
| `output/trin1.html` | Formular, trin 1: Hvad vil du donere? (tæller pr. møbeltype) |
| `output/trin2.html` | Formular, trin 2: Hvornår kan vi hente? (dato, gadeplan, billeder, kommentar) |
| `output/trin3.html` | Formular, trin 3: Hvem skal vi kontakte? (navn, adresse, telefon) |
| `output/kvittering.html` | Kvittering efter bestilling |
| `output/aflever-selv.html` | Aflevér selv: find en butik |
| `output/automatiske-mails.html` | De automatiske mails til donoren ved accept og afvisning |
| `output/admin.html` | Admin-siden "Donationer til genbrug" (tabel, modal, datovælger, køreplan) |
| `afhentninger-admin.html` | Samme som `output/admin.html` – arbejdsfilen, der bygges af rk-ui-design-skill'en |
| `Anmodninger om afhentning-html.zip` | Første eksport fra Claude Design (29/10) – kun til reference |

Alle filer i `output/` er selvstændige HTML-filer (CSS, JS, ikoner og Gotham-fonten ligger inde i filen) og kan uploades direkte til en webserver. Formularens sider linker til hinanden med relative links, så de skal ligge i samme mappe. Eneste eksterne afhængighed: donorbillederne i `admin.html` hentes fra Unsplash og kræver internetforbindelse.

Formular og admin er prototyper med testdata: der sendes ikke noget nogen steder hen, og ændringer gemmes kun i browserens hukommelse.

## Ændringer

### 2026-11-06

- Ny `index.html` samler formular, admin og auto-mails i én fil med smal, mørk navigation. Formularens trin 1 hedder nu `trin1.html`.
- Kvittering: ny tekst fra "Donationssystem - tekster.docx". Ny fil `automatiske-mails.html` viser mails ved accept og afvisning.
- Uploadet til `lindsteen/donationsprototype` (GitHub Pages). Forsiden er nu formularen; admin er flyttet til `/admin.html`.
- Formularen er responsiv: fra 768 px går header og footer i fuld bredde, indholdet står i en centreret kolonne (maks. 760 px), og knapperne står nederst til højre. Mobilvisningen er uændret.
- Formularen: Støt-knappen og burgermenuen i headeren er fjernet.
- Formular, trin 1: "Næste" og "Din donation" skjules, når der ikke er valgt noget.
- Formular, trin 1: "Tilføj genstand som ikke er på listen" giver en ny række med tekstfelt og antal – én pr. klik. Mangler navnet ved klik på Næste, vises en fejl.
- Formular, trin 3: feltet "Hvordan vil du gerne kontaktes?" (SMS/E-mail/Opkald) er fjernet.
- Admin: titlen er "Donationer til genbrug"; logoet er mindre og centreret i headeren.
- Admin, modal: rækken "Kontakt via" er fjernet.
- Admin-lærredet i Claude Design er omdøbt til "Donationer til genbrug - backend" og opdateret til den nyeste udgave af admin-siden.
- `output/`-mappen oprettet med upload-klare udgaver af alle sider.

### 2026-10-29

- Admin-siden bygget om efter MRK-designet "Udvidet frivillighåndtering" (Figma), men som selvstændig platform uden MRK's header og menu.
- Tabel med Donor (navn, vej, telefon), Møbler, Info, Status og Note; faste kolonnebredder.
- Filtre: I gang (Ny + Accepteret + Planlagt, standard), Nye, Accepteret, Planlagt, Afsluttede. Statussen "Åben for andre" er udgået.
- Status-dropdown med farver fra Hjælpelinjen-designet: Ny lyserød (#FFC3C3), Accepteret grøn, Planlagt orange (#FFDE90), Afhentet grå, Afvist grå-beige. Valglisten er hvid.
- Info-kolonnen viser "Modtaget/Accepteret/Afhentet/Afvist X dage siden" eller "Planlagt dd.mm.åå kl. 13–18".
- Bred modal med alle oplysninger, 3 billeder pr. række med billedviser (klik → stort, frem/tilbage), status, "Planlagt afhentning" med datovælger (dato + mellem kl./og kl.) – valg af tidspunkt sætter status til Planlagt – og noter, der fylder højden ud.
- "Næste skridt" afhænger af status: Ny (Accepter/Afvis), Accepteret (tekst + Afvis), Planlagt (tekst + Afvis), afsluttede (skjult). Accepter/Afvis gemmer, lukker modalen og viser en 5 sekunders toast ("Donationen er accepteret. Donoren får automatisk besked").
- "Print køreplan": vælg køredato i kalender (datoer med afhentninger er markeret), liste med navn, adresse og tidspunkt øverst og alle øvrige oplysninger (uden billeder); printvenlig udskrift.
- 20 testanmodninger med forskellige statusser.
