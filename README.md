# Build-week-1
  

🎯 Quiz Application
Un'applicazione quiz interattiva, randomizzata e timer-based
Font: Roboto  ·  Background: Epicode Theme

📋 Indice
Descrizione
Tecnologie
Struttura dell'App
Funzionalità
Funzioni Implementate
Logica del Quiz
Team & Divisione del Lavoro
📝 Descrizione
Applicazione web single-page che guida l'utente attraverso un quiz di 10 domande con risposte multiple. Le domande e le opzioni vengono presentate in ordine randomizzato ad ogni avvio. Un timer visivo con icona a clessidra accompagna ogni domanda, imponendo un ritmo di gioco dinamico.

🛠 Tecnologie
Stack	Descrizione
HTML5	Struttura semantica della pagina
CSS3	Styling con font Roboto e background Epicode
JavaScript (Vanilla)	Logica applicativa, randomizzazione, timer, localStorage
🏗 Struttura dell'App
L'intera applicazione è gestita all'interno di un unico container #app, il cui contenuto viene aggiornato dinamicamente in base alla variabile currentScreen.

Struttura della schermata Quiz
<p>   → Numero domanda
<h3>  → Titolo della domanda
<div> → Bottoni risposta
⏳    → Timer con clessidra affiancata
Schermate disponibili
Schermata	Descrizione
Welcome	Schermata di benvenuto con call-to-action per iniziare il quiz
Quiz	Itera 10 volte in ordine randomizzato. Mostra numero domanda, titolo, risposte e timer
Results	Schermata finale con punteggio totale e diagramma riassuntivo
✨ Funzionalità
🎲 Randomizzazione — domande e risposte vengono mescolate ad ogni sessione
⏳ Timer — countdown visivo con icona a clessidra affiancata al testo
🎨 Feedback visivo immediato:
✅ Risposta corretta → bottone verde
❌ Risposta errata → bottone rosso + illuminazione della risposta corretta
⏰ Tempo scaduto → evidenziazione della risposta corretta + registrazione errore + avanzamento automatico
📊 Diagramma finale — visualizzazione grafica dei risultati (non barre)
💾 Persistenza — salvataggio del punteggio finale in localStorage
⚙️ Funzioni Implementate
Funzione	Descrizione
render()	Router principale: controlla currentScreen e invoca la funzione di rendering corretta
renderWelcome()	Costruisce e inietta la schermata di benvenuto
renderQuiz()	Renderizza la domanda corrente: numero <p>, titolo <h3>, bottoni risposta, timer con clessidra
renderResults()	Genera la schermata finale con punteggio e diagramma
startTimer()	Avvia il countdown tramite setInterval
stopTimer()	Interrompe il countdown tramite clearInterval
handleAnswer()	Colora i bottoni (verde/rosso), aggiorna il punteggio, attende FEEDBACK_DELAY ms prima di procedere
handleTimeUp()	Gestisce la scadenza del tempo: registra errore, evidenzia risposta corretta, avanza
advance()	Passa alla domanda successiva o, se completate tutte le 10, reindirizza ai risultati
saveResults()	Salva il punteggio finale dell'utente nel localStorage
🧠 Logica del Quiz
Randomizzazione
All'avvio del quiz, l'array QUESTIONS viene mescolato
Ad ogni domanda viene assegnato un id univoco dalla coppia rendering prima dell'inizio
Le risposte di ogni singola domanda vengono a loro volta randomizzate prima della visualizzazione
Ciclo di vita di una domanda
renderQuiz() → startTimer()
      │
      ├─ Risposta data → handleAnswer() → [feedback FEEDBACK_DELAY ms] → advance()
      │
      └─ Tempo scaduto → handleTimeUp() → [mostra corretta] → advance()
                                                    │
                                          ultima domanda?
                                          ├─ Sì → saveResults() → renderResults()
                                          └─ No → renderQuiz()
👥 Team & Divisione del Lavoro
Coppia Rendering — Alberto & Gabriele
render() · renderWelcome() · renderQuiz() · renderResults()

Aggiungono gli id alle domande nell'array QUESTIONS
Comunicano a tutto il team i nomi delle classi CSS usate prima che gli altri inizino
Logica Risposte — Manuel
handleAnswer() · advance()

Gestisce il feedback visivo e l'avanzamento dopo 1500ms
Si coordina con la coppia sulla struttura DOM di renderQuiz()
Timer — Nicole
startTimer() · stopTimer() · handleTimeUp()

Gestisce la logica della clessidra (l'animazione CSS è assegnata al CSS)
CSS — Yhara
Welcome · Quiz · Results · Clessidra

Aspetta i nomi delle classi dalla coppia prima di iniziare
Area	Classi principali
CSS Welcome	Stili schermata iniziale
CSS Quiz	Domanda, bottoni, timer, counter, .correct / .wrong
CSS Results	Percentuale, diagramma, verdetto
CSS Clessidra	Icona e animazione del timer
Da assegnare — saveResults()
Suggerimento: assegnare a Manuel, contiguo ad advance()

Salva il punteggio finale in localStorage. Se il tempo lo consente, aggiungere il confronto dettagliato domande giuste/sbagliate.

Build Week 1 — Epicode · Team 1