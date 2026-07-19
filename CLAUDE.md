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
  fine giornata (le stats di ieri vanno in `history`, max 60 giorni); lo stato
  viene salvato subito dopo il load
- Timer pomodoro: `startTimer/pauseTimer/finishPhase`, fasi
  idle|work|short_break|long_break, anello SVG di progresso
- Check-in "stai lavorando?" a intervallo durante il focus
- Promemoria fissi a orario (`checkReminders`): confronto "orario superato e non
  ancora sparato oggi" (resiste al throttling in background), flag `workdaysOnly`
- Promemoria periodici (`checkPeriodics`): acqua/gambe/20-20-20, a intervallo
- Giorni lavorativi vs festivi: lun-ven meno festività italiane (Pasqua con
  algoritmo di Gauss), override manuale giornaliero in `dayOverrides`
- Storico settimanale (`renderHistory`): grafico a barre ultimi 7 giorni
  (minuti focus, oggi evidenziato, distrazioni, totali settimana)
- Export `.ics` dei promemoria fissi (RRULE daily o MO-FR) per il calendario del
  telefono
- Wake Lock opzionale durante il focus; catch-up su `visibilitychange`
- PWA: `manifest.json`, `sw.js` (cache-first con aggiornamento in rete), `icons/`

## Come testare
Serve un server HTTP per il service worker:
`python -m http.server 8000` nella cartella, poi aprire `http://localhost:8000`.
I test finora sono stati fatti con Playwright + Chromium (caricamento senza
errori JS, cicli timer, filtro feriali/festivi, rollover giornaliero, grafico
storico, export .ics). Trucco per testare: seminare
`localStorage.focusAppState_v1` via `page.evaluate` e ricaricare.

## Stato (handoff del 2026-07-19, sera)
- `main` = app completa: PR #1 (storico settimanale) **mergiata**; CLAUDE.md incluso
- Vecchia PR #1 su Dalamar90/Projects **chiusa senza merge** (codice migrato qui)
- Branch remoto `claude/statistiche-storico` mergiato, cancellabile dalla UI
  GitHub (solo cosmetica)
- A cura dell'utente: attivare GitHub Pages (Settings → Pages → `main`, `/ (root)`)
  per installare la PWA dal telefono all'URL
  https://dalamar90.github.io/Focus-Timer-ADHD/

## Roadmap migliorie (discussa con l'utente, in ordine consigliato)
Piccole ad alto impatto ADHD:
1. **Parcheggio pensieri**: campo sempre visibile per annotare pensieri intrusivi
   senza uscire dal focus; ritrovabili a fine giornata nel registro
2. **Durate rapide**: chip 15/25/45/90 min accanto al timer (energia variabile,
   modalità hyperfocus da 90')
3. **Check-in a intervallo casuale** (es. 8–15 min) invece che fisso, contro
   l'assuefazione
4. Rumore bianco/marrone in focus (Web Audio API già in uso, niente file)
5. Scorciatoie tastiera (spazio = avvia/pausa, D = distrazione)

Medie:
6. Micro-passi per task (checklist dentro la priorità, contro la task paralysis)
7. Barra della giornata (posizione dell'ora attuale tra inizio/fine lavoro,
   contro la time blindness)
8. Heatmap oraria delle distrazioni (utile anche per calibrare orari farmaci)
9. Export/backup dati in JSON (il localStorage si perde svuotando i dati browser)
10. Streak gentile, mai colpevolizzante

Grande:
11. Notifiche push reali ad app chiusa (serve piccolo backend Web Push, es.
    Cloudflare Workers) — unica via per promemoria farmaci affidabili al 100%
