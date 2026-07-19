# Focus Assistant — contesto per Claude

## Cos'è
PWA single-page (tutto in `index.html`: markup + CSS + JS, zero dipendenze esterne)
per aiutare l'utente a mantenere il focus lavorando con l'ADHD. UI in italiano.
Proprietario: Dalamar90. Cartella di lavoro locale dell'utente:
`D:\Pregetti Marco\Focus-Timer-ADHD` (Windows).

## Vincoli di design (non violare)
- **Un solo file HTML autonomo**: niente CDN, niente font/script esterni, niente
  build step. Tutto lo stato in `localStorage` (chiave `focusAppState_v1`),
  nessun dato lascia il browser.
- UI e testi in italiano; toni gentili, mai colpevolizzanti (utente ADHD:
  il pulsante distrazioni è volutamente "senza giudizio").
- Accessibilità: aria-label sugli input generati dinamicamente, focus-visible,
  prefers-reduced-motion, target tocco ≥ 40px.

## Architettura (dentro index.html, IIFE unica)
- `loadState()/saveState()` — stato + migrazioni retrocompatibili + rollover di
  fine giornata (le stats di ieri vanno in `history`, max 60 giorni)
- Timer pomodoro: `startTimer/pauseTimer/finishPhase`, fasi
  idle|work|short_break|long_break, anello SVG di progresso
- Check-in "stai lavorando?" a intervallo durante il focus
- Promemoria fissi a orario (`checkReminders`): confronto "orario superato e non
  ancora sparato oggi" (resiste al throttling in background), flag `workdaysOnly`
- Promemoria periodici (`checkPeriodics`): acqua/gambe/20-20-20, a intervallo
- Giorni lavorativi vs festivi: lun-ven meno festività italiane (Pasqua con
  algoritmo di Gauss), override manuale giornaliero in `dayOverrides`
- Export `.ics` dei promemoria fissi (RRULE daily o MO-FR) per il calendario del
  telefono
- Wake Lock opzionale durante il focus; catch-up su `visibilitychange`
- PWA: `manifest.json`, `sw.js` (cache-first con aggiornamento in rete), `icons/`

## Come testare
Serve un server HTTP per il service worker:
`python -m http.server 8000` nella cartella, poi aprire `http://localhost:8000`.
I test finora sono stati fatti con Playwright + Chromium (caricamento senza
errori JS, cicli timer, filtro feriali/festivi, rollover giornaliero, export
.ics). Trucco per testare: seminare `localStorage.focusAppState_v1` via
`page.evaluate` e ricaricare.

## Stato al momento dell'handoff (2026-07-19)
- `main` = app completa e funzionante
- **PR #1 aperta** (branch `claude/statistiche-storico`): card "Ultimi 7 giorni"
  con grafico a barre + archiviazione automatica dello storico. Testata, in
  attesa di review/merge dell'utente.
- Da fare a cura dell'utente: attivare GitHub Pages (Settings → Pages → main,
  root) per installare la PWA dal telefono; chiudere la vecchia PR #1 su
  Dalamar90/Projects (codice ormai migrato qui).

## Idee future già discusse
- Suoni ambientali/rumore bianco durante il focus
- Check-in a intervallo casuale invece che fisso
- Notifiche push reali ad app chiusa (richiede backend Web Push)
