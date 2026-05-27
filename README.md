
<p align="center">
<img src="https://img.shields.io/badge/Quiz-App-blueviolet?style=for-the-badge&logo=javascript&logoColor=white" />
<img src="https://img.shields.io/badge/Status-Work%20In%20Progress-yellow?style=for-the-badge" />
<img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />
</p>

<h1 align="center">🎯 Quiz Application</h1>
<p align="center">
<em>Un'applicazione quiz interattiva, randomizzata e timer-based</em><br>
<strong>Font:</strong> Roboto &nbsp;·&nbsp; <strong>Background:</strong> Epicode Theme
</p>

---

## 📋 Indice

- [Descrizione](#-descrizione)
- [Tecnologie](#-tecnologie)
- [Struttura dell'App](#-struttura-dellapp)
- [Funzionalità](#-funzionalità)
- [Funzioni Implementate](#-funzioni-implementate)
- [Logica del Quiz](#-logica-del-quiz)
- [Team & Divisione del Lavoro](#-team--divisione-del-lavoro)

---

## 📝 Descrizione

Applicazione web single-page che guida l'utente attraverso un quiz di **10 domande** con risposte multiple.
Le domande e le opzioni vengono presentate in **ordine randomizzato** ad ogni avvio.
Un **timer visivo** con icona a clessidra accompagna ogni domanda, imponendo un ritmo di gioco dinamico.

---

## 🛠 Tecnologie

| Stack | Descrizione |
|---|---|
| `HTML5` | Struttura semantica della pagina |
| `CSS3` | Styling con font **Roboto** e background Epicode |
| `JavaScript (Vanilla)` | Logica applicativa, randomizzazione, timer, localStorage |

---

## 🏗 Struttura dell'App

L'intera applicazione è gestita all'interno di un unico container `#app`, il cui contenuto viene aggiornato dinamicamente in base alla variabile **`currentScreen`**.

### Struttura della schermata Quiz

```
<p>   → Numero domanda
<h3>  → Titolo della domanda
<div> → Bottoni risposta
⏳    → Timer con clessidra affiancata
```

### Schermate disponibili

| Schermata | Descrizione |
|---|---|
| **Welcome** | Schermata di benvenuto con call-to-action per iniziare il quiz |
| **Quiz** | Itera 10 volte in ordine randomizzato. Mostra numero domanda, titolo, risposte e timer |
| **Results** | Schermata finale con punteggio totale e diagramma riassuntivo |

---

## ✨ Funzionalità

- 🎲 **Randomizzazione** — domande e risposte vengono mescolate ad ogni sessione
- ⏳ **Timer** — countdown visivo con icona a clessidra affiancata al testo
- 🎨 **Feedback visivo immediato:**
  - ✅ Risposta corretta → bottone **verde**
  - ❌ Risposta errata → bottone **rosso** + illuminazione della risposta corretta
  - ⏰ Tempo scaduto → evidenziazione della risposta corretta + registrazione errore + avanzamento automatico
- 📊 **Diagramma finale** — visualizzazione grafica dei risultati (non barre)
- 💾 **Persistenza** — salvataggio del punteggio finale in `localStorage`

---

## ⚙️ Funzioni Implementate

| Funzione | Descrizione |
|---|---|
| `render()` | Router principale: controlla `currentScreen` e invoca la funzione di rendering corretta |
| `renderWelcome()` | Costruisce e inietta la schermata di benvenuto |
| `renderQuiz()` | Renderizza la domanda corrente: numero `<p>`, titolo `<h3>`, bottoni risposta, timer con clessidra |
| `renderResults()` | Genera la schermata finale con punteggio e diagramma |
| `startTimer()` | Avvia il countdown tramite `setInterval` |
| `stopTimer()` | Interrompe il countdown tramite `clearInterval` |
| `handleAnswer()` | Colora i bottoni (verde/rosso), aggiorna il punteggio, attende `FEEDBACK_DELAY` ms prima di procedere |
| `handleTimeUp()` | Gestisce la scadenza del tempo: registra errore, evidenzia risposta corretta, avanza |
| `advance()` | Passa alla domanda successiva o, se completate tutte le 10, reindirizza ai risultati |
| `saveResults()` | Salva il punteggio finale dell'utente nel `localStorage` |

---

## 🧠 Logica del Quiz

### Randomizzazione

1. All'avvio del quiz, l'array `QUESTIONS` viene mescolato
2. Ad ogni domanda viene assegnato un `id` univoco dalla coppia rendering prima dell'inizio
3. Le risposte di ogni singola domanda vengono a loro volta randomizzate prima della visualizzazione

### Ciclo di vita di una domanda

```
renderQuiz() → startTimer()
      │
      ├─ Risposta data → handleAnswer() → [feedback FEEDBACK_DELAY ms] → advance()
      │
      └─ Tempo scaduto → handleTimeUp() → [mostra corretta] → advance()
                                                    │
                                          ultima domanda?
                                          ├─ Sì → saveResults() → renderResults()
                                          └─ No → renderQuiz()
```

---

## 👥 Team & Divisione del Lavoro

### Coppia Rendering — Alberto & Gabriele

> `render()` · `renderWelcome()` · `renderQuiz()` · `renderResults()`

- Aggiungono gli `id` alle domande nell'array `QUESTIONS`
- Comunicano a tutto il team i nomi delle **classi CSS** usate prima che gli altri inizino

---

### Logica Risposte — Manuel

> `handleAnswer()` · `advance()`

- Gestisce il feedback visivo e l'avanzamento dopo `1500ms`
- Si coordina con la coppia sulla struttura DOM di `renderQuiz()`

---

### Timer — Nicole

> `startTimer()` · `stopTimer()` · `handleTimeUp()`

- Gestisce la logica della clessidra (l'animazione CSS è assegnata al CSS)

---

### CSS — Yhara

> Welcome · Quiz · Results · Clessidra

- Aspetta i nomi delle classi dalla coppia prima di iniziare

| Area | Classi principali |
|---|---|
| CSS Welcome | Stili schermata iniziale |
| CSS Quiz | Domanda, bottoni, timer, counter, `.correct` / `.wrong` |
| CSS Results | Percentuale, diagramma, verdetto |
| CSS Clessidra | Icona e animazione del timer |

---

### Da assegnare — `saveResults()`

> Suggerimento: assegnare a Manuel, contiguo ad `advance()`

Salva il punteggio finale in `localStorage`. Se il tempo lo consente, aggiungere il confronto dettagliato domande giuste/sbagliate.

---

<p align="center">
<sub>Build Week 1 — Epicode · Team 1</sub>
</p>
