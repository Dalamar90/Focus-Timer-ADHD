# Product

## Register

product

## Users

Utente singolo (Marco) con ADHD che usa l'app come assistente alla concentrazione durante la giornata lavorativa. Contesto d'uso: tenuta aperta in una scheda del browser (desktop e smartphone, PWA installabile) mentre lavora ad altro. Deve poter dare un'occhiata veloce e capire in un colpo d'occhio "a che punto sono, cosa sto facendo, quanto manca" senza fermarsi a ragionare. Interfaccia in italiano.

## Product Purpose

Timer Pomodoro pensato per l'ADHD: struttura il tempo in sessioni di focus e pause, tiene ancorato l'utente al compito con check-in "stai lavorando?", conta pomodori/minuti/distrazioni della giornata, e gestisce promemoria (farmaci, idratazione, stacco, regola 20-20-20) con notifiche del browser. Successo = l'utente resta concentrato più a lungo, non perde i promemoria importanti, e apre l'app senza sentirsi sopraffatto.

## Brand Personality

Energico e motivante, ma mai rumoroso. Deve dare spinta e senso di progresso (il conto alla rovescia e l'anello sono il cuore emotivo), restando abbastanza sobrio da non diventare esso stesso una fonte di distrazione. Tre parole: **motivante, chiaro, affidabile**. L'energia arriva dal colore d'accento, dalla gerarchia forte e dal feedback sui traguardi — non da decorazioni gratuite.

## Anti-references

- Dashboard SaaS corporate piene di card identiche impilate (freddo, generico, "generato").
- App gamificate iper-stimolanti (coriandoli, badge, animazioni ovunque): per un utente ADHD sono controproducenti.
- Produttività sovraccarica di opzioni sempre visibili (tipo cruscotti densi): la configurazione deve stare in secondo piano rispetto al fare.

## Design Principles

1. **Il timer è il protagonista.** Tutto il resto è di supporto; la gerarchia visiva deve renderlo ovvio senza leggere.
2. **Colpo d'occhio prima di tutto.** Stato, fase e tempo restante leggibili in mezzo secondo, da lontano, anche su schermo piccolo.
3. **Energia senza rumore.** Movimento e colore usati per comunicare stato e traguardi, mai come decorazione. Ogni animazione ha una controparte reduced-motion.
4. **La configurazione si fa da parte.** Promemoria e impostazioni sono disponibili ma visivamente subordinati al focus attivo.
5. **Feedback che gratifica.** Completare un pomodoro deve dare una piccola soddisfazione tangibile; è ciò che tiene agganciato l'utente.

## Accessibility & Inclusion

Target WCAG AA. Priorità dichiarata dall'utente: **testo più grande e leggibile, contrasto alto** — niente grigi slavati per il testo informativo. Mantenere quanto già presente: gestione `prefers-reduced-motion`, focus visibile, etichette ARIA, `aria-live` sugli stati del timer, target touch ≥44px. La distinzione tra fasi (focus/pausa) non deve affidarsi al solo colore.
