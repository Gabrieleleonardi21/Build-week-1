<p align="center">
  <img src="https://img.shields.io/badge/Quiz-Tech-c49000?style=for-the-badge&logo=javascript&logoColor=white" />
  <img src="https://img.shields.io/badge/Status-Completato-4caf50?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />
</p>

<h1 align="center">Quiz Tech</h1>
<p align="center">
  <em>Un quiz interattivo su tecnologia e informatica — timer, shuffle, feedback visivo e molto altro</em><br>
  <strong>Build Week 1 — Epicode · Team 1</strong>
</p>

---

## Indice

- [Descrizione](#descrizione)
- [Tecnologie](#tecnologie)
- [Struttura del progetto](#struttura-del-progetto)
- [Schermate](#schermate)
- [Funzionalità](#funzionalità)
- [Configurazione](#configurazione)
- [Avvio](#avvio)
- [Team](#team)

---

## Descrizione

**Quiz Tech** è una web app single-page che mette alla prova le conoscenze di tecnologia e informatica attraverso **20 domande a risposta multipla** (incluse vero/falso) con timer, shuffling automatico e feedback istantaneo.

Al termine viene mostrata una schermata dei risultati con grafico a torta, verdetto promosso/bocciato, riepilogo di tutte le risposte e la possibilità di lasciare una valutazione con le 🍌.

---

## Tecnologie

| Stack | Utilizzo |
|---|---|
| `HTML5` | Struttura semantica della pagina |
| `CSS3` | Layout, animazioni, responsive design |
| `JavaScript ES Modules` | Logica applicativa, rendering dinamico, localStorage |
| `canvas-confetti` (CDN) | Animazione coriandoli alla promozione |
| `Google Fonts — Roboto` | Tipografia |

---

## Struttura del progetto

```
Build-week-1/
├── index.html
├── questions.json
└── assets/
    ├── css/
    │   └── style.css
    ├── js/
    │   └── script.js
    └── img/
        ├── epicode-logo.png
        └── bg.jpg
```

Le domande sono caricate da `questions.json` tramite `fetch` all'avvio; il file è modificabile senza toccare il codice.

---

## Schermate

### Welcome
Mostra titolo, descrizione e regole del quiz (numero domande, secondi per risposta, soglia di superamento). Il pulsante **Inizia** avvia la sessione resettando score e cronologia in `localStorage`.

### Quiz
Per ogni domanda vengono mostrati:
- Contatore `Domanda X / 20`
- Timer con icona clessidra (⌛) che conta alla rovescia da 20 secondi; diventa rosso sotto i 5 secondi
- Testo della domanda
- Fino a quattro bottoni risposta con lettera (A / B / C / D) in ordine casuale

Alla selezione di una risposta:
- Tutti i bottoni vengono disabilitati immediatamente
- Il bottone scelto diventa **verde** (corretto) o **rosso** (errato)
- Se errato, la risposta corretta viene evidenziata in verde
- Dopo 2 secondi si avanza automaticamente

Se il tempo scade senza risposta, la domanda è registrata come sbagliata, la risposta corretta viene evidenziata e si avanza dopo 2 secondi.

### Risultati
- Toast con GIF animata e verdetto **Promosso!** / **Bocciato!** che appare e poi svanisce
- Coriandoli (`canvas-confetti`) in caso di promozione
- Messaggio di esito e badge colorato **Promosso!** / **Bocciato**
- Grafico a torta CSS-only (`conic-gradient`) con percentuale al centro
- Riepilogo `X / 20 risposte corrette`
- Lista di tutte le domande con icona ✓ / ✗; per le risposte errate viene mostrata la risposta corretta
- Pulsanti **Riprova** e **Lascia un voto**

### Feedback
- Valutazione con 5 emoji 🍌: hover per anteprima, click per bloccare il voto, secondo click sulla stessa per toglierlo
- GIF animata che cambia in base al voto selezionato (1–5)
- Il voto viene salvato in `localStorage` alla chiave `quizRating`
- Premendo **Invia voto**: se è stato espresso un voto appare un toast di ringraziamento, poi si torna alla schermata di benvenuto

---

## Funzionalità

| Funzionalità | Dettaglio |
|---|---|
| Shuffle domande | Array mescolato con Fisher-Yates ad ogni sessione |
| Shuffle risposte | Le opzioni di ogni domanda vengono riordinate casualmente |
| Timer per domanda | 20 secondi; urgenza visiva sotto i 5 secondi |
| Feedback immediato | Verde/rosso sui bottoni + evidenziazione risposta corretta anche allo scadere del tempo |
| Cronologia sessione | Ogni risposta salvata in `localStorage` (`quizHistory`) e letta dalla schermata risultati |
| Grafico a torta | Costruito solo con CSS (`conic-gradient`) |
| Toast risultato | Overlay con GIF e messaggio; compare e svanisce con animazione (fade-in 2s, visibile 1.5s, fade-out 1.2s) |
| Confetti | Attivato solo in caso di promozione |
| Rating con emoji | 5 🍌 con hover, selezione, toggle e GIF per ogni livello; persistito in `localStorage` |
| Toast feedback | Ringraziamento animato dopo l'invio del voto |
| Responsive | Layout adattivo per tablet (≤ 768 px) e mobile (≤ 480 px) |

---

## Configurazione

Le costanti principali sono in cima a [assets/js/script.js](assets/js/script.js):

```js
const TOTAL_QUESTIONS = QUESTIONS.length; // numero domande da questions.json (20)
const PASS_THRESHOLD = 60;                // % minima per essere promosso
const TIMER_DURATION = 20;               // secondi per domanda
const FEEDBACK_DELAY = 2000;            // ms di attesa dopo la risposta prima di avanzare
```

Per aggiungere o modificare domande basta editare [questions.json](questions.json) mantenendo la struttura:

```json
{
  "id": "q01",
  "question": "Testo della domanda",
  "correct_answer": "Risposta corretta",
  "incorrect_answers": ["Opzione A", "Opzione B", "Opzione C"]
}
```

Per le domande vero/falso `incorrect_answers` conterrà un solo elemento.

---

## Avvio

`script.js` usa `fetch` e i moduli ES, quindi richiede un server HTTP (non funziona con `file://`).

**Con VS Code** — installa l'estensione *Live Server* e clicca **Go Live**.

**Con Node.js:**

```bash
npx serve .
```

**Con Python:**

```bash
python3 -m http.server 8080
```

Poi apri `http://localhost:8080` nel browser.

---

## Team

| Membro | Contributo |
|---|---|
| **Alberto** | Rendering schermate, struttura DOM |
| **Gabriele** | Rendering schermate, struttura DOM |
| **Manuel** | Logica risposte, avanzamento, `handleAnswer` |
| **Nicole** | Timer, `startTimer`, `stopTimer`, `handleTimeUp` |
| **Yhara** | CSS — Welcome, Quiz, Results, animazione clessidra |

---

<p align="center">
  <sub>Build Week 1 — Epicode · Team 1</sub>
</p>

