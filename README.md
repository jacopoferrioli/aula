# Assemblea - FERRIOLI.EU

Applicazione web leggera per simulare la gestione di un’assemblea. HTML, CSS e JavaScript, senza build. La realizzazione è puramente a scopo ricreazionale e di ricerca, i nomi rappresentati sono fittizi e non rappresentano nessuna reale Istituzione.

## Prova immediata

Apri `dist/index.html` nel browser e scegli **Prova la presidenza · demo locale**. Da **Impostazioni → Carica dati dimostrativi** puoi caricare una seduta fittizia. La demo salva i dati nel browser; non sincronizza computer diversi. Il cambio del ruolo demo permette di provare anche il votante (email fittizia `votante@example.test`).

## Funzioni

- Seduta: apertura, sospensione con orario e conto alla rovescia, ripresa, conclusione.
- Ordine del giorno e discussione; interventi per numero del posto, coda, pausa e aggiunta di tempo, sforamento luminoso.
- Componenti, presenze e diritto di voto.
- Mozioni ed emendamenti, voto palese/segreto, raccolta manuale/digitale.
- Preparazione → apertura → chiusura → scrutinio → pubblicazione. I conteggi non compaiono nell’interfaccia prima dello scrutinio; il tabellone li mostra solo dopo la pubblicazione.
- Maggioranza semplice, assoluta, qualificata o soglia personalizzata, con quorum. Presenze e basi di calcolo sono fotografate all’apertura.
- Verbale con interventi, cronologia, sospensioni e risultati pubblicati. **Salva come PDF** apre la stampa del browser: su macOS seleziona **PDF → Salva come PDF**.

## Firebase

La configurazione web del progetto `ferriolieu` fornita dall’utente è inclusa in `dist/firebase-config.js`. Authentication usa Email/Password; non viene attivato Analytics. Questa versione carica gli SDK Firebase 11.10.0 da gstatic quando si effettua l’accesso. Eventuali configurazioni salvate manualmente in precedenza nel browser hanno la precedenza.

Il progetto deve avere Authentication con Email/Password attivo e Realtime Database creato e accessibile agli account di prova. Gli account devono esistere già. L’app utilizza esclusivamente i percorsi `aula/session` e `aula/ballots` e gestisce una seduta condivisa alla volta. Non modifica automaticamente le regole del database. Un progetto Firebase di test separato evita sovrapposizioni con dati reali.

Ruoli:

- `jacopo@ferrioli.eu`: presidente.
- `amministrazione.generale@cas.ferrioli.eu`, `amministrazione@ferrioli.eu`: segretari.
- Altri account: votanti. L’email deve figurare tra i componenti presenti aventi diritto.
- **Tabellone**: **Apri tabellone** apre una scheda separata (`?view=tabellone`) in sola visualizzazione. Mantieni aperta la regia nello stesso browser/profilo: timer, sospensioni e risultati pubblicati si aggiornano tramite eventi storage. Funziona anche senza Realtime Database. Il tabellone non richiede un secondo login; non riceve risultati non pubblicati. Puoi trascinare la scheda su un secondo monitor e selezionare **Schermo intero**.

Verifica del 26 ottobre 2026: il servizio Authentication riconosce il progetto; Realtime Database risponde HTTP 423 (database disattivato). Il login con credenziali utente non è stato eseguito. Dopo un accesso riuscito, se il database non risponde entro 7 secondi o rifiuta la connessione, l’app mantiene l’accesso e lavora in locale. Per collegare dispositivi diversi occorre riattivare Realtime Database e accedere nuovamente. Il controllo dei ruoli e la riservatezza dei conteggi sono volutamente a livello d’interfaccia, per la simulazione richiesta. Non costituisce un sistema per elezioni reali. La sincronizzazione della regia scrive l’intera seduta: per il testing evita modifiche simultanee di presidente e segretario. I voti sono scritti separatamente per utente.

## Verifica

Controllata la sintassi JavaScript e verificati ruoli, presenze, maggioranze, quorum, risultati nascosti/pubblicati, sforamento del timer e registrazione degli interventi. Verificati anche apertura del tabellone separato, permanenza della regia, sincronizzazione di timer e sospensioni e trasferimento dei soli risultati pubblicati. Collaudo visivo non completato per indisponibilità dell’automazione del browser.

## Pubblicazione e dominio

Vedi [PUBBLICAZIONE.md](PUBBLICAZIONE.md). Il repository include un workflow GitHub Actions che pubblica `dist` su GitHub Pages. Il dominio personalizzato va configurato nelle impostazioni Pages e nel DNS.
