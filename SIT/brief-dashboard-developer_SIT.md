# Brief tecnico — Dashboard strategica "Two Engines"
### Documento per il front-end developer

> **Lingua:** istruzioni in italiano · **tutto il testo a schermo (UI copy) in inglese** — la dashboard è mostrata a due General Manager anglofoni.
> **Uso:** presentazione dal vivo in screen-share durante un colloquio + link inviabile dopo. Pubblico **non-marketing** (commerciale/manageriale): priorità a chiarezza, prevedibilità, professionalità. Niente gergo, niente fronzoli.
> **Consegna tecnica:** un singolo file HTML/CSS/JS autonomo, nessun reload di pagina, nessuna dipendenza esterna se non i web font. Deve funzionare da desktop (screen-share) e in modo dignitoso da mobile.

---

## 1. Concetto in una frase

Una **sola schermata** con **due "volani"** (DMC e The Malta Experience). L'utente clicca un volano: questo va in primo piano, l'altro arretra. Poi, **un bottone alla volta**, l'utente rivela i livelli successivi — che **restano impilati** mentre lui spiega. Mai mostrare tutto insieme. È una **presentazione interattiva guidata**, non una pagina da leggere.

---

## 2. Modello di interazione (il cuore — leggere con attenzione)

**Regola d'oro:** un livello appare solo quando l'utente preme un bottone. I livelli già aperti **rimangono visibili e si impilano** verticalmente. Niente cambia mai pagina.

### Stati

**STATO 0 — Home**
- Due blocchi affiancati: **DMC** (sinistra) e **The Malta Experience** (destra), di pari dimensione.
- Ogni blocco mostra solo: **titolo + sottotitolo + obiettivo (una riga)**.
- Sotto entrambi, a tutta larghezza, una **banda-basamento** (vedi §5C).
- Tra i due blocchi, una **freccia a senso unico** da DMC → TME (vedi §5B).

**STATO 1 — Volano in focus** (es. click su DMC)
- Il blocco cliccato (DMC) **si ingrandisce e si centra**.
- L'altro blocco (TME) **arretra**: scala a ~55%, opacità ~35%, scivola di lato. Resta cliccabile (cliccandolo si scambia il focus).
- Sotto il titolo del blocco in focus compare: **un sottotitolo descrittivo + il primo bottone di reveal**.

**STATI 2→5 — Reveal progressivo (uno alla volta)**
- Ogni pressione del bottone fa **apparire UN solo nuovo livello**, che si inserisce **sotto** i precedenti (stack verticale che cresce verso il basso).
- Il livello appena aperto porta **in fondo a sé** il bottone per aprire il livello successivo.
- I livelli precedenti **restano visibili** (non si sostituiscono, non si chiudono).
- Al reveal: auto-scroll morbido fino a portare in vista il nuovo livello.
- Sequatza dei reveal per ciascun volano (5 step): **Objective → Audiences → The cycle → Message & channels → KPIs**. Vedi contenuti in §4.
- Dopo l'ultimo livello (KPIs) non c'è più bottone "avanti": fine catena.

**Reset / indietro**
- Un controllo **"← Back"** sempre visibile in alto nello stato focus: chiude tutti i livelli aperti e torna allo STATO 0 (i due blocchi pari).
- Da lì l'utente può cliccare l'altro volano e ripetere lo stesso identico percorso.

### Diagramma di stato (testuale)
```
HOME (2 blocchi pari)
  └─click DMC──► DMC in focus, TME arretra, mostra [Objective] + bottone
        └─btn──► + [Audiences] (impilato) + bottone
              └─btn──► + [The cycle] + bottone
                    └─btn──► + [Message & channels] + bottone
                          └─btn──► + [KPIs]  (fine)
        └─Back──► HOME
  └─click TME──► (identico, percorso speculare)
```

---

## 3. Gerarchia visiva e layout

- **Desktop:** STATO 0 = due colonne affiancate (50/50) + banda basamento sotto. STATO focus = il volano in focus occupa la colonna centrale (~640px max), l'altro ridotto a lato.
- **Mobile (<760px):** STATO 0 = i due blocchi impilati (DMC sopra, TME sotto), freccia verticale tra essi, basamento in fondo. In focus: il volano selezionato a tutta larghezza, l'altro collassa in una piccola barra cliccabile in cima ("◄ The Malta Experience").
- I livelli rivelati sono **card impilate** dentro l'area del volano in focus, con generosa aria tra loro.
- Massimo respiro: niente densità da cruscotto tecnico. Spazio bianco abbondante.

---

## 4. Contenuti a schermo (UI copy — in inglese, testo definitivo)

> Tutto il testo seguente va a schermo **così com'è**. È volutamente breve: pubblico non-marketing.

### VOLANO A — DMC

- **Title:** `DMC — Special Interest Travel`
- **Subtitle:** `The trust engine · B2B`
- **Objective (riga sempre visibile):** `Generate qualified B2B pipeline that feeds sales and revenue.`

**Reveal 1 — Audiences** · intestazione: `Who we speak to`
- `MICE planners & event agencies` — *(incl. incentive houses, PCOs)*
- `Leisure tour operators` — *(France first → China / Japan / Italy / Spain)*
- `Corporates & associations` — *(direct)*

**Reveal 2 — The cycle** · intestazione: `The lead cycle`
Mostrare come ciclo/loop a 5 nodi (vedi §5A):
`Reach → Capture (MQL) → Nurture → Sales enablement (SQL) → Win → ↻ referrals feed Reach`

**Reveal 3 — Message & channels** · intestazione: `What we say & where`
- **Messaggio core (evidenziato, grande):** `"We take the risk out of your event."`
- *(sotto-riga, più piccola):* `Security · low risk · resolved complexity · 45 years of flawless execution.`
- **Channels (riga di chip, secondari, sotto):** `Buyer-intent SEO` · `Trade networks (euromic, Cvent, Travelmediate)` · `LinkedIn + targeted ABM` · `Trade shows / fam trips` · `Referrals`

**Reveal 4 — KPIs** · intestazione: `The numbers` *(conversion rates)*
- `Site visit → enquiry`
- `Enquiry → MQL`
- `MQL → SQL`
- `SQL → won deal`

---

### VOLANO B — The Malta Experience

- **Title:** `The Malta Experience`
- **Subtitle:** `The demand engine · B2C / e-commerce`
- **Objective:** `Capture existing tourist demand and win direct bookings — recover margin from OTAs and fill the show.`

**Reveal 1 — Audiences** · intestazione: `Who we speak to`
> **Importante (resa visiva):** le due audience **non** sono pari per volume. Rendere ② visibilmente più "grande/pesante" di ① (es. card più larga o barra-volume). Non dargli pari dimensione.
- `Groups from the DMC` — *(predictable base load · ~zero acquisition cost · in-group margin)* — **card piccola**
- `Independent tourists (FIT)` — *(the real volume · incl. cruise & others)* — **card grande**

**Reveal 2 — The cycle** · intestazione: `The visitor cycle`
Ciclo a 4 nodi:
`Capture intent → Convert to direct booking → Fill the show (yield) → Retain & advocate → ↻ reviews & data feed Capture`

**Reveal 3 — Message & channels** · intestazione: `What we say & where`
- **Messaggio core (evidenziato, grande):** `"Understand 7,000 years of Malta in 45 minutes — the first thing to do, in 17 languages, booked in one tap."`
- *(sotto-riga):* `Desire + ease — not security. Skip-the-queue · guaranteed seat · best price direct.`
- **Channels per tipo di domanda (due gruppi distinti, sotto):**
  - `Aware demand →` `Google (Search · Maps · SEO)`
  - `Latent demand →` `Meta + TikTok`
  - *(nota a schermo, piccola):* `OTAs = reach, not the goal.`

**Reveal 4 — KPIs** · intestazione: `The numbers` *(e-commerce funnel)*
- `Site visit → add to cart`
- `Cart → checkout`
- `Checkout → purchase`
- `Direct vs OTA mix` — *(the margin story)*

---

### CONNESSIONE (sempre visibile in Home; vedi §5B–C)

- **Freccia DMC → TME (senso unico), label al passaggio del mouse / sotto la freccia:**
  `Groups delivered by the DMC become high-margin, zero-cost visitors to The Malta Experience.`
- **Banda basamento (sotto entrambi i volani), titolo + 4 voci:**
  - Titolo: `Built once, owned by the Group`
  - `Shared measurement` · `Shared first-party data` · `Brand consistency` · `Competitor & market watch`

---

## 5. Elementi visivi specifici

### 5A — I "volani" / cicli
- Renderli come **loop circolare** di nodi etichettati con frecce che tornano all'inizio (per comunicare "si auto-alimenta"). In alternativa, se il cerchio risulta troppo fitto su mobile, **stepper orizzontale** con una freccia di ritorno tratteggiata dall'ultimo al primo nodo.
- Nodi semplici (pallino + etichetta). Niente icone decorative inutili.

### 5B — Freccia di connessione
- Una **singola freccia a senso unico** da DMC (sinistra) verso TME (destra). Spessa, in `--red` (vedi palette). Mai bidirezionale.

### 5C — Banda basamento
- Banda orizzontale a tutta larghezza **sotto** entrambi i volani, in **blu** `--blue`, che visivamente "regge" i due blocchi (i blocchi colorati sembrano poggiarci sopra). Comunica: fondamenta condivise del gruppo. Titolo bianco grande ammesso; corpo in `--ink`.

---

## 6. Design system

**Palette del brand (CSS variables):**
```
/* Colori brand forniti dal cliente */
--blue:      #5D9ACB;  /* blu brand */
--orange:    #FBAF5C;  /* arancio brand — titoli */
--white:     #FFFFFF;  /* bianco — testo SOLO su fondi scuri/saturi */
--red:       #CB2B1C;  /* accento */
--green:     #8FBA27;  /* accento 1 */

/* Helper derivati — NECESSARI per la leggibilità (vedi ⚠️ sotto) */
--blue-deep: #2C5A85;  /* blu scurito: SOLO questo regge il testo bianco */
--ink:       #16242E;  /* testo scuro per superfici chiare */
--surface:   #FFFFFF;  /* superficie chiara delle card di contenuto */
```

**Mappatura d'uso — COLOR-BLOCKING (i due motori sono blocchi colorati):**
- **Blocco DMC** = riempimento **arancio** `--orange`, **testo scuro** `--ink` (titoli + corpo). Mai testo bianco qui.
- **Blocco The Malta Experience** = riempimento **verde** `--green`, **testo scuro** `--ink`. Mai testo bianco qui.
- **Basamento condiviso** = **blu** `--blue` (è la base su cui poggiano i due motori — fondamenta del gruppo). Regge un titolo **bianco grande**; per il corpo, testo `--ink`.
- **Freccia di connessione + highlight del messaggio core** = **rosso** `--red`. È l'unico fondo su cui il **testo bianco** è ammesso.
- **Canvas / sfondo pagina** = chiaro/neutro (`--surface` o un grigio-azzurro pallido), così i blocchi colorati risaltano e tutto resta leggibile. **Non** un fondo blu pieno dietro i blocchi (diventa chiassoso).
- *Refinement opzionale:* per non affaticare, i grandi riempimenti possono usare una versione leggermente più tenue del colore, con il colore pieno su header/bordo del blocco.

> ⚠️ **NOTA CONTRASTO — VINCOLO, non opzionale.**
> - Testo su arancio/verde → **scuro** (`--ink`), ≈ 6–8:1 ✅. Bianco su arancio/verde ≈ 2:1 ❌ (vietato).
> - Bianco ammesso **solo** su `--red` (≈ 5:1 ✅) e su `--blue` solo per testo grande/bold.
> - **Mai** titoli arancioni su fondo blu, **mai** testo bianco su blu chiaro `#5D9ACB` (1,5–2,8:1, illeggibili).
> - Ogni testo deve raggiungere ≥4,5:1 (corpo) / ≥3:1 (titoli grandi).

**Tipografia (Google Fonts):**
- Tutto in **Roboto** — pesi 400 / 500 / 700.
- *Nota onesta:* scelta sicura e legibilissima, ma è un font "default" senza carattere distintivo. Accettabile per un pubblico manageriale che premia chiarezza; rinuncia però alla raffinatezza "premium".

**Tono visivo:** professionale, pulito, minimale. Molto spazio bianco. Ombre morbide, bordi sottili, angoli arrotondati ~12–14px. La saturazione dei colori brand va **dosata**: ampie superfici chiare, colore come accento — non muri di blu/arancio/rosso/verde insieme.

---

## 7. Animazioni (CSS, sobrie)

- **Focus/recede:** transizione ~450ms ease su scala + opacità + posizione del blocco non in focus.
- **Reveal livello:** fade-in + slide-up di ~14px, ~450ms. Un livello alla volta.
- **Auto-scroll** morbido al nuovo livello dopo il reveal.
- **Bottoni:** hover con leggero sollevamento/illuminazione; chiari e affordanti (es. label `▸ Show who we speak to`, poi `▸ Show the cycle`, ecc.).
- Niente animazioni a comparsa multiple simultanee, niente parallax, niente effetti che distraggano un pubblico manageriale.

---

## 8. Etichette dei bottoni di reveal (UI copy, inglese)

In ordine, per ciascun volano:
1. `▸ Show who we speak to`
2. `▸ Show the cycle`
3. `▸ Show what we say & where`
4. `▸ Show the numbers`

Controllo ritorno: `← Back`

---

## 9. Fuori scope / note

- **Nessun dato reale nei KPI:** mostrare i KPI come **etichette di ciò che misureremo**, non come numeri. (I numeri non esistono ancora: manca il tracking.) Non inventare percentuali.
- Nessun backend, nessun login, nessuno storage. Tutto statico e client-side.
- Accessibilità di base: contrasto adeguato, navigabile da tastiera, `aria` sui bottoni.

---

## 10. Riassunto per il developer in 5 righe

1. Una pagina, mai reload. Su canvas chiaro: **blocco DMC arancione** e **blocco The Malta Experience verde** (testo scuro su entrambi), poggiati su un **basamento blu**, con **freccia rossa** a senso unico DMC→TME. Bianco solo sul rosso. Mai testo bianco/arancio su blu chiaro.
2. Click su un blocco → va in focus, l'altro arretra.
3. Quattro bottoni in sequenza rivelano **un livello alla volta**, che **si impila** (Objective è già visibile; poi Audiences, Cycle, Message&channels, KPIs).
4. I livelli aperti restano; "← Back" azzera e torna ai due blocchi pari.
5. Tutto il testo a schermo è quello del §4, in inglese, invariato.
