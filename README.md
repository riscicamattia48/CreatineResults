# Registro Peso — Creatina

Webapp statica a singolo file per tracciare il peso corporeo durante l'assunzione di creatina, con grafico dell'andamento e fascia evidenziata per il range atteso di ritenzione idrica nelle prime 3-4 settimane.

- Nessun backend, nessuna build: è un unico file `index.html` (HTML + CSS + JS inline).
- I dati vengono salvati in `localStorage`, quindi restano **sul dispositivo/browser** in cui apri la pagina. Se apri il sito da più dispositivi, avrai uno storico separato per ciascuno (non c'è sincronizzazione tra dispositivi in questa versione).

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
