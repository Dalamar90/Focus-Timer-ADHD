# Considerazioni future — usabilità e struttura

Note raccolte dall'utente (Marco) da approfondire nelle prossime sessioni.
Tema comune: la pagina unica è diventata troppo lunga e mette in fondo cose
secondarie, mentre ciò che serve durante l'uso (il timer e le sue impostazioni)
deve stare a portata di mano.

## ✅ Fatto (2026-07-21)
Ristrutturazione dell'architettura dell'informazione in 3 viste JS con barra di
navigazione fissa in basso (Focus / Promemoria / Dati), sempre dentro l'unico
`index.html`. Copre i punti 1–4 qui sotto:
- **Focus**: timer + durata rapida (chip 15/25/45/90 + campo con bottone
  «Applica») + priorità del giorno + stats di oggi (punti 3 e 4).
- **Promemoria**: promemoria fissi (+ export .ics) e periodici, fuori dal flusso
  del focus (punto 1).
- **Dati**: storico «Ultimi 7 giorni», registro di oggi, impostazioni timer
  avanzate (punto 2).
I punti seguenti restano come traccia storica del ragionamento.

## 1. Promemoria periodici → pagina dedicata
Nella pagina principale, in fondo, sono di ingombro e poco utili lì.
Spostarli in una **pagina/vista apposita**, raggiungibile ma fuori dal flusso
del focus.

## 2. Storico ("Ultimi 7 giorni") → pagina dedicata
Anche lo storico non serve mentre si lavora: portarlo in una **pagina/vista
apposita** insieme (o vicino) agli altri dati di riepilogo.

## 3. Impostazioni timer vicino al timer
Oggi le impostazioni (durata lavoro/pause, cicli, check-in) sono in fondo,
dentro un `<details>`: **così non sono utilizzabili**. Devono stare **accanto
al timer** — di lato o subito sotto — così da poter regolare la durata mentre
si guarda il timer. È l'azione più frequente e va resa immediata.

## 4. Modifica durata tramite bottone
Per cambiare la durata: campo/controllo rapido vicino al timer + un **bottone
esplicito** per applicare la modifica (conferma chiara invece di modifica al
volo). Collegato al punto 3.

---

## Direzione di lavoro
Questi punti spingono verso una **ristrutturazione dell'architettura
dell'informazione**: da pagina-unica-che-scorre a una struttura con
- schermata "focus" essenziale (timer + impostazioni rapide + priorità del giorno),
- viste separate per promemoria e storico (es. tab in basso o menu).

Approccio suggerito: **ragionare come farebbe l'utente** (cosa serve durante
il focus vs cosa si consulta ogni tanto), oppure appoggiarsi a una skill di
usabilità/UX per impostare la nuova struttura prima di scrivere codice.
Candidate: `/impeccable shape` (progettare il flusso prima di costruire),
oppure gli skill di design UX disponibili (design-critique, user-research).

Vincoli da mantenere: resta un **unico file `index.html`** autonomo, niente
dipendenze esterne, stato in `localStorage`, UI in italiano, toni gentili
(ADHD). Le "pagine" possono essere viste/schermate gestite in JS, non file HTML
separati.
