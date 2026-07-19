# Focus Assistant (ADHD-friendly)

Progressive Web App (PWA) single-page pensata come tecnica del pomodoro "più
strutturata": timer di focus, check-in periodici, promemoria fissi e micro-pause
ricorrenti, con orari che si adattano a giorni lavorativi e festivi/weekend.

## Come si usa

**In browser (subito, senza installare nulla):** apri `index.html` (doppio click, o
trascinalo nella finestra del browser) e tienilo aperto in una scheda mentre lavori.
Alla prima apertura clicca "Attiva" per dare il permesso alle notifiche del browser.

**Come app installata (PWA):** per installarla sul telefono con l'icona in home,
il browser richiede che i file siano serviti via **HTTPS** (non basta aprire il file
locale). Il modo più semplice è pubblicare questa cartella con **GitHub Pages**:

1. Nel repo su GitHub: `Settings → Pages → Deploy from a branch`
2. Branch: `main`, cartella `/ (root)`
3. Apri l'URL risultante (https://dalamar90.github.io/Focus-Timer-ADHD/) dal browser
   del telefono → menu → **"Aggiungi a schermata Home"** (Android/Chrome) o
   **Condividi → "Aggiungi a Home"** (iOS/Safari)

Una volta installata, l'app ha icona propria, si apre a schermo intero e funziona
offline grazie al service worker (`sw.js`).

**Importante sui promemoria mentre l'app non è in primo piano:** i timer e i
check-in interni richiedono la scheda/app aperta — è un limite dei browser, non
essendoci un server con notifiche push dietro. Per i promemoria a orario fisso
(farmaci, "tra poco stacchi") c'è però una via più affidabile: l'**export nel
calendario del telefono** (vedi sotto), che usa le notifiche native del calendario
anche ad app chiusa.

## Funzionalità

- **Timer strutturato**: lavoro / pausa breve / pausa lunga, con durate e numero di
  cicli configurabili (default 25/5/15, pausa lunga ogni 4 cicli).
- **Check-in periodico**: durante il focus, ogni tot minuti (default 10) appare un
  popup "Stai lavorando?" con due risposte veloci: sì o distratto/a. Le risposte
  finiscono nel registro e nelle statistiche del giorno.
- **Promemoria fissi**: preimpostati alle 9:10 e 14:10 ("prendi i farmaci", tutti i
  giorni) e alle 13:45 e 17:45 ("tra poco stacchi", solo giorni lavorativi). Orari,
  testo e il flag "solo feriali" sono modificabili dalla sezione "Promemoria fissi",
  e puoi aggiungerne altri.
- **Promemoria periodici** (nuovi): a intervallo regolare durante la giornata,
  indipendenti dal timer pomodoro — pensati per le micro-pause che si dimenticano
  facilmente:
  - 💧 Bevi un po' d'acqua (ogni 45 min di default)
  - 🚶 Sgranchisciti le gambe (ogni 60 min)
  - 👀 Regola 20-20-20 per gli occhi: ogni 20 minuti, guarda un punto lontano ~6
    metri per 20 secondi
  Ognuno è configurabile (intervallo, testo, attivo/disattivo, solo feriali).
- **Giorno lavorativo vs festivo**: un badge in alto mostra se oggi è considerato
  giorno lavorativo (lun-ven, esclusi festivi nazionali italiani calcolati
  automaticamente — incl. Pasquetta) o festivo/weekend, con possibilità di
  correggerlo manualmente per la giornata (es. ferie infrasettimanali, lavoro di
  sabato). I promemoria marcati "solo feriali" seguono questo stato.
- **Export calendario (.ics)**: genera e scarica un file `.ics` con i promemoria
  fissi come eventi ricorrenti (ogni giorno, o solo lun-ven se "solo feriali"),
  pronto da importare nel calendario del telefono (Google Calendar, Apple Calendar,
  ecc.) per avere notifiche native anche ad app chiusa. I promemoria periodici
  restano gestiti dall'app, dato che un calendario pieno di eventi ogni 20 minuti
  non sarebbe leggibile.
- **Priorità di oggi**: fino a 3 task, con selezione del task attivo su cui si sta
  lavorando in quel momento.
- **Log distrazioni**: pulsante rapido per segnare una distrazione senza rompere il
  flow, senza bisogno di aprire il check-in.
- **Statistiche del giorno**: pomodori completati, minuti di focus, distrazioni
  loggate. Si azzerano automaticamente il giorno dopo.
- **Storico settimanale**: grafico a barre degli ultimi 7 giorni con minuti di
  focus per giorno (oggi evidenziato), numero di distrazioni e totali della
  settimana. A fine giornata le statistiche vengono archiviate automaticamente
  (storico conservato fino a 60 giorni).

Tutto lo stato (impostazioni, task, promemoria, statistiche) è salvato nel
`localStorage` del browser: resta sul tuo dispositivo, nessun dato lascia la pagina.

## File del progetto

- `index.html` — l'app (markup, stile e logica in un unico file)
- `manifest.json` — metadati PWA (nome, icone, tema) per l'installazione
- `sw.js` — service worker: cache dell'app shell per l'uso offline
- `icons/` — icone dell'app (192px, 512px, 512px maskable per Android)

## Idee per il futuro

- Suoni ambientali / rumore bianco durante le sessioni di focus
- Modalità "check-in casuale" invece che a intervallo fisso
- Notifiche push reali anche ad app completamente chiusa (richiede un piccolo
  backend con Web Push, non solo un service worker statico)
