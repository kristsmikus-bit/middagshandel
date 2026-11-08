# Middagshandel

Handleliste-app for kollektivet. Du legger inn hvor mange som spiser torsdag, fredag, lørdag og søndag, og appen regner ut innkjøpslista for riktig uke i firerukersrotasjonen. Lista kan deles rett til Slack.

Appen er helt statisk: bare HTML, CSS og JavaScript. Ingen server, ingen innlogging, ingen nøkler. Alt som trengs er at filene i denne mappa ligger på en nettadresse med https.

## Filene

| Fil | Hva den gjør |
|---|---|
| `index.html` | Hele appen, inkludert menydata og beregning |
| `manifest.webmanifest` | Gjør at appen kan legges på hjemskjermen |
| `sw.js` | Gjør at appen virker uten nett etter første besøk |
| `icon*.png`, `icon.svg`, `apple-touch-icon.png` | Ikoner |

## Legg den ut på nett (GitHub Pages, gratis)

1. Lag en konto på github.com om du ikke har.
2. Lag et nytt offentlig repository, for eksempel `middagshandel`.
3. Velg **Add file → Upload files** og dra inn alle filene i denne mappa. Trykk **Commit changes**.
4. Gå til **Settings → Pages**. Under *Build and deployment* velger du *Deploy from a branch*, branch `main`, mappe `/ (root)`. Lagre.
5. Etter et minutt er appen på `https://<brukernavn>.github.io/middagshandel/`.

Alternativ: Cloudflare Pages eller Netlify har også gratis «dra og slipp»-opplasting av en mappe og gir en https-adresse.

## Del med kollektivet

Send lenken i Slack. På telefonen velger man **Del → Legg til på Hjem-skjerm** (iPhone) eller **Installer app** (Android). Da åpner den som en vanlig app, uten adressefelt og uten innlogging.

## Oppdatere menyen

Menyene ligger øverst i `index.html` under `const MENU`. Hver rett har en liste med varer, og hver vare har mengder for 12, 16 og 17 personer slik de står på de utskrevne handlelistene. Rett i fila og last opp på nytt. Bump gjerne `CACHE`-navnet i `sw.js` (for eksempel til `middagshandel-v2`) så alle får ny versjon med en gang.

## Ukerotasjon

Appen vet hvilken handleliste-uke det er ved å telle uker fra et kjent punkt: kalenderuke 46 i 2026 er handleliste uke 3. Blir rotasjonen forskjøvet (for eksempel etter en ferie), kan hver bruker rette det under **Innstillinger** i appen. Vil du endre det for alle, rett `DEFAULT_STATE.anchor` i `index.html` og øk `anchorVersion` med én.
