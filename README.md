# Registro Peso — Creatina

Webapp statica a singolo file per tracciare il peso corporeo durante l'assunzione di creatina, con grafico dell'andamento e fascia evidenziata per il range atteso di ritenzione idrica nelle prime 3-4 settimane.

- Nessun backend, nessuna build: solo file statici (`index.html`, `manifest.json` e le icone), tutti nella root del repo — nessuna sottocartella.
- I dati vengono salvati in `localStorage`, quindi restano **sul dispositivo/browser** in cui apri la pagina. Se apri il sito da più dispositivi, avrai uno storico separato per ciascuno (non c'è sincronizzazione tra dispositivi in questa versione).

## Struttura del repo

```
creatine-tracker/
├── index.html        webapp (self-contained)
├── manifest.json      web app manifest (icona su schermata Home / PWA)
├── icon.svg           sorgente vettoriale dell'icona
├── icon-16.png         favicon
├── icon-32.png         favicon
├── icon-180.png        apple-touch-icon (iOS)
├── icon-192.png        manifest / Android
├── icon-512.png        manifest / Android (alta risoluzione)
├── wordmark.svg        logo orizzontale (icona + testo), per README o pagine esterne
└── wordmark.png
```

Su iPhone, aprendo il sito in Safari e usando "Aggiungi a Home", l'icona `icon-180.png` verrà usata automaticamente grazie al `manifest.json` e al tag `apple-touch-icon`.

## Pubblicare su GitHub Pages

1. Crea un nuovo repository su GitHub (es. `creatine-tracker`) e carica il file `index.html` nella root del repo.
2. Vai su **Settings → Pages**.
3. In "Source" seleziona il branch `main` (o `master`) e la cartella `/ (root)`.
4. Salva. Dopo qualche minuto la pagina sarà disponibile su:
   `https://<tuo-username>.github.io/<nome-repo>/`

## Uso locale

Basta aprire `index.html` direttamente nel browser (doppio click), oppure servirlo con un server statico qualsiasi, ad esempio:

```bash
python3 -m http.server 8000
```

e visitare `http://localhost:8000`.

## Personalizzazione

Tutto il codice (stili, markup, logica) è in `index.html`. I punti principali:

- `STORAGE_KEY` — chiave usata in `localStorage` per salvare le rilevazioni.
- Variabili CSS in `:root` — palette colori (dark/light theme automatico in base alle preferenze di sistema).
- Funzione `drawChart()` — disegna il grafico SVG dell'andamento, inclusa la fascia del range atteso (attualmente giorni 0-21, +0/+2 kg dal peso di partenza).

## Backup dei dati

Essendo i dati solo locali (`localStorage`), se cambi browser o cancelli i dati di navigazione li perdi. Se vuoi un backup, puoi esportare manualmente lo storage da console del browser:

```js
copy(localStorage.getItem('creatine-weight-log-v1'))
```

e reimportarlo su un altro dispositivo con:

```js
localStorage.setItem('creatine-weight-log-v1', '<contenuto copiato>')
```
