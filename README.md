# FT8 Waterfall Tracker 📡

Web app gratuita e statica per gamificare le live FT8 su Twitch: mappa mondo
colorabile "a waterfall" (come un SDR), conteggio DXCC, distanza record,
locatori unici, obiettivo di sessione, boss fight su un DX raro, bingo DXCC
e toast animati "rarità" (comune/raro/epico/leggendario) ad ogni contatto.

Tutto gira nel browser, i dati restano salvati in locale (localStorage):
nessun server, nessun account, nessun backend da mantenere.

## 🚀 Pubblicarla su GitHub Pages

1. Crea un repository (es. `ft8-tracker`) e carica questi 4 file nella root:
   `index.html`, `manifest.json`, `icon.svg`, `README.md`.
2. Vai su **Settings → Pages**, sorgente "Deploy from branch", branch `main`,
   cartella `/ (root)`. Salva.
3. Dopo un minuto la app sarà online su
   `https://<tuo-utente>.github.io/ft8-tracker/`.

Puoi anche solo aprire `index.html` in locale con doppio click, funziona
comunque (serve internet solo per caricare la mappa e i font al volo).

## 🎥 Come usarla in diretta su Twitch

1. In OBS aggiungi una **Browser Source** puntata all'URL della pagina.
2. Per interagire con la mappa (cliccare gli stati, aprire il pannello)
   senza uscire da OBS: **tasto destro sulla fonte → Interact**. Da lì puoi
   cliccare/scrivere esattamente come in un browser normale, e i tuoi
   spettatori vedranno tutto in tempo reale.
3. In alternativa apri la pagina in una finestra Chrome normale su un
   secondo monitor e catturala in OBS con **Window Capture**: più comodo se
   registri anche con mouse/tastiera fisici.
4. Aggiungendo `?clean=1` all'URL (es. `.../index.html?clean=1`) nascondi
   l'ingranaggio ⚙️ e il footer, per un overlay ancora più pulito — utile se
   vuoi comunque tenere aperta una seconda scheda "di controllo" senza
   `?clean=1` per loggare i contatti mentre l'overlay resta pulito.

## 🎮 Come funziona il gioco

- **Log manuale**: dato che l'FT8 non parte in automatico dal tuo software
  di logging, apri il pannello (icona ⚙️ o tasto `C`), scrivi lo stato
  collegato (autocompletamento incluso), e volendo nominativo, locatore
  (grid, es. `JN63`) e distanza in km. Premi "Registra contatto".
- Ogni contatto colora lo stato sulla mappa con un colore più "caldo" più
  contatti accumuli su quel paese (proprio come l'intensità di un waterfall
  SDR: verde → ambra → rosso).
- **Rarità automatica**: in base alla distanza, ogni contatto genera un
  toast a schermo (comune/raro/epico/leggendario). Le soglie km sono
  modificabili dal pannello.
- **Obiettivo di sessione**: imposta es. "10 nuovi paesi stasera", la barra
  si riempie ad ogni nuovo QSO registrato da quel momento in poi.
- **Boss fight**: scegli un DX molto raro come "boss" della serata (es.
  Antartide); lampeggia sulla mappa finché non lo colleghi.
- **Bingo DXCC**: 25 paesi target (mix facili + aspirazionali) che si
  spuntano da soli man mano che li colleghi — buono anche come clip per
  TikTok quando lo completi.
- **Esporta/Importa backup**: dal pannello puoi scaricare un file `.json`
  con tutta la cronologia (utile prima di cambiare PC/browser, o per tenere
  uno storico "carriera" separato dalle singole live).
- **Reset sessione** azzera solo il contatore "sessione odierna" e il
  timer; **Reset totale** cancella tutto (richiede conferma).

## 🔧 Personalizzazione veloce

- Lista bingo: modifica l'array `BINGO_LIST` dentro `index.html`.
- Soglie rarità di default: variabile `DEFAULT_STATE.thresholds`.
- Palette colori: variabili CSS in cima al file (`:root { --phosphor: ... }`).

## Nota tecnica

La mappa usa [D3.js](https://d3js.org/) + [world-atlas](https://github.com/topojson/world-atlas)
caricati da CDN (jsDelivr) al volo — serve quindi una connessione internet
attiva quando apri la pagina, anche se poi tutto il resto (dati, contatori)
funziona offline grazie al `localStorage` del browser.
