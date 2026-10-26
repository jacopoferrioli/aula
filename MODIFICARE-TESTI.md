# Modificare i testi direttamente su GitHub

## Testi principali

Apri [dist/testi.js](https://github.com/jacopoferrioli/aula/blob/main/dist/testi.js), premi la matita **Edit this file**, modifica le frasi tra virgolette e premi **Commit changes** sul branch `main`.

Il file raccoglie nome predefinito dell’assemblea, titolo e descrizione del login, pulsante di accesso, titolo della presidenza e testi introduttivi dei partecipanti. Mantieni i nomi delle proprietà, le virgole e le parentesi. Per andare a capo nel login usa `\n`. Per una virgoletta dentro una frase usa `\"`, oppure le virgolette tipografiche « ».

Il nome di una seduta già salvata è un dato: modificalo in **Impostazioni → Nome dell’assemblea**. Cambiare `nomeAssemblea` nel codice definisce il nome delle nuove sedute; non rinomina quelle già salvate.

## Altri file

| File | Cosa contiene |
| --- | --- |
| [dist/app.js](https://github.com/jacopoferrioli/aula/blob/main/dist/app.js) | Testi secondari di pulsanti, finestre, verbale e tutta la logica dell’app. Cerca la frase esatta e cambia solo il testo. |
| [dist/index.html](https://github.com/jacopoferrioli/aula/blob/main/dist/index.html) | Titolo della scheda (`<title>`) e descrizione del sito. |
| [dist/style.css](https://github.com/jacopoferrioli/aula/blob/main/dist/style.css) | Colori, caratteri, spaziature e impaginazione. |
| [dist/firebase-config.js](https://github.com/jacopoferrioli/aula/blob/main/dist/firebase-config.js) | Configurazione tecnica Firebase, non testi visibili. |

Ogni commit su `main` avvia la pubblicazione automatica. Controlla [Actions](https://github.com/jacopoferrioli/aula/actions), attendi il segno verde e ricarica il sito. Se vedi ancora la vecchia versione, su macOS usa **⌘⇧R**.
