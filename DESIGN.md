# Design

Sistema visivo di Focus Assistant. Tema scuro unico, registro **product**: il design serve il compito (concentrarsi), con un'energia motivante concentrata nel timer.

## Theme

Dark-only. Sfondo profondo con un alone radiale tenue in alto che dà profondità senza rumore. L'energia arriva dal colore d'accento e dal bagliore dell'anello quando il timer è attivo, non da decorazioni diffuse.

## Color

Token CSS in `:root` (index.html).

| Ruolo | Token | Valore | Uso |
|---|---|---|---|
| Sfondo | `--bg` | `#0f1118` | body (con gradiente radiale verso `--bg-grad` `#161a26`) |
| Superficie | `--panel` | `#1b1e28` | card primarie |
| Superficie 2 | `--panel-2` | `#272c3a` | input, stat, badge, toast |
| Hover | `--panel-hover` | `#313749` | hover su superfici |
| Testo | `--text` | `#f2f4fa` | contenuto principale |
| Testo attenuato | `--text-dim` | `#a8afc6` | label, sottotitoli (≥7.6:1 su panel) |
| Accento / Focus | `--accent` | `#6d8bff` | CTA, fase focus, selezione |
| Accento forte | `--accent-strong` | `#5573ff` | hover CTA |
| Pausa | `--good` | `#57cf95` | fase pausa |
| Allerta | `--bad` | `#ff7a7a` | distrazione, stop |
| Festivo | `--accent-2` | `#ffb454` | indicatore giorno festivo |

Strategia: **Restrained** (product). L'accento marca solo azioni primarie, selezione e stato. Le fasi focus/pausa sono distinte da colore **e** da forma (pallino + etichetta testuale), mai dal solo colore. Contrasto verificato: corpo ≥7:1, placeholder ≥4.5:1.

## Typography

Un'unica famiglia (system-ui / SF / Segoe). Base **17px** per leggibilità (esigenza dichiarata). Scala fissa in rem, non fluida.

- Timer `.ring-time`: 3rem / 750, tabular-nums — l'elemento più grande della pagina.
- H1: 1.6rem / 750, `text-wrap: balance`.
- Titoli card `h2`: sentence-case, 1.1rem / 700, `--text` (niente maiuscolo tracciato "eyebrow"). Nelle sezioni di configurazione (`.card--config h2`) più discreti: 1rem / 650, `--text-dim`.
- Statistiche: valore 1.9rem / 750 (il primo in `--accent`), label 0.82rem.
- Corpo/label: 0.9–0.95rem.

## Layout

`.wrap` max 720px, singola colonna. Gerarchia a due livelli:

- **Primario** (`.card`): timer (hero), Priorità di oggi, Oggi (statistiche) — superficie piena.
- **Configurazione** (`.card--config`): registro, promemoria, impostazioni — sfondo trasparente con bordo tenue, si fanno da parte.

Il timer (`.timer-card`) è trattato come hero distinto: raggio maggiore, gradiente sottile, ombra elevata, non "una card tra le tante".

## Components

- **Anello timer**: `stroke` 13px, `stroke-linecap: round`. In esecuzione riceve un `drop-shadow` che fa da bagliore (blu in focus, verde in pausa). Pallino di fase nell'etichetta come indicatore non-cromatico.
- **Bottoni**: raggio 12px, min-height 46px (touch). `.btn-primary` = accento con ombra soffusa e lift in hover. Feedback `active: scale(0.96)`.
- **Controlli del timer**: il controllo principale (Avvia idle / Pausa in esecuzione) è la CTA dominante su riga propria (`.btn-row--primary`, min-height 54px); Salta e Reset sono ghost piccoli sotto (`.btn-row--secondary`). La gerarchia "cosa premo ora" è immediata.
- **Badge giorno / toast**: superficie piena con bordo sottile e pallino di stato — nessuna banda laterale colorata.
- **Modali**: overlay scuro, pannello `--panel`, CTA in accento.

## Motion

150–450ms, curve ease-out (`cubic-bezier(0.22,1,0.36,1)`). La motion comunica stato/traguardo, mai decorazione:

- Bagliore anello alla partenza; transizione di colore fase 0.4s.
- **Celebrazione** a fine pomodoro: pulse dell'anello (`ringPulse`) + bump delle statistiche (`statBump`).
- Tutte le animazioni hanno la controparte `@media (prefers-reduced-motion: reduce)` (durata azzerata).

## Accessibility

WCAG AA. Focus visibile (outline `--accent-2`), etichette ARIA, `aria-live` sugli stati del timer, target touch ≥44px, distinzione fasi non solo cromatica. Vedi principi in [PRODUCT.md](PRODUCT.md).
