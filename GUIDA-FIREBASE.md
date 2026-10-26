# Configurare Realtime Database per Aula

Il progetto è **ferriolieu**. La configurazione web è già inclusa nel codice: non occorre incollarla nel sito. Non serve Firestore.

## 1. Account di accesso

Apri https://console.firebase.google.com/project/ferriolieu/authentication/providers

In **Authentication → Sign-in method**, abilita **Email/Password**. In **Users**, verifica che esistano gli account che vuoi usare (oppure aggiungili con **Add user**):

- `jacopo@ferrioli.eu`: presidente.
- `amministrazione.generale@cas.ferrioli.eu` e `amministrazione@ferrioli.eu`: segretari.
- Gli altri account: votanti.

Usa le password degli account Firebase. Il sito non crea automaticamente nuovi utenti.

## 2. Database

Apri https://console.firebase.google.com/project/ferriolieu/database

Seleziona **Realtime Database**, poi il database `ferriolieu-default-rtdb`, regione Europe West 1. Il suo indirizzo è:

`https://ferriolieu-default-rtdb.europe-west1.firebasedatabase.app`

Se compare **Enable / Riattiva database**, riattivalo. Se vedi `null` nella scheda **Data / Dati**, è semplicemente vuoto. Non devi creare a mano nodi, tabelle o collezioni: l’app salva `aula/session` e `aula/ballots` quando la usi.

## 3. Regole

In **Realtime Database → Rules / Regole**, trovi un documento JSON. Nel repository il file [database.rules.json](database.rules.json) contiene regole semplici compatibili con questa app.

Se il database è dedicato solo ad Aula, copia tutto il contenuto del file nell’editor e premi **Publish / Pubblica**. Salvare il file su GitHub non cambia automaticamente le regole Firebase.

Se il database ospita altre applicazioni, conserva le loro regole e aggiungi il blocco `aula` dentro `rules`. Non sovrascrivere tutto. Eventuali autorizzazioni globali `".read": true` o `".write": true` alla radice prevalgono sui limiti dei percorsi figli: non garantirebbero le restrizioni descritte qui.

Queste regole permettono agli utenti autenticati di leggere la seduta, al presidente e ai due segretari di modificarla e a ciascun utente di registrare il proprio voto. Sono regole di base per la simulazione: la segretezza prima della pubblicazione e il controllo completo dello stato di voto restano gestiti dall’interfaccia.

Riferimenti: https://firebase.google.com/docs/database/security/rules-conditions e https://firebase.google.com/docs/reference/security/database

## 4. Domini

In **Authentication → Settings → Authorized domains**, aggiungi `jacopoferrioli.github.io` e il tuo dominio personalizzato quando lo usi. Inserisci solo il dominio, senza `https://` e senza `/aula/`.

## 5. Prova completa

1. Apri il sito GitHub Pages e accedi come `jacopo@ferrioli.eu`.
2. Dopo il collegamento, in **Impostazioni → Connessione** deve comparire **Connesso · aggiornamenti in tempo reale**.
3. Apri **Partecipanti**, lascia la modalità numerica, inserisci per esempio 30 presenti, 5 assenti, 2 presenti senza diritto e 0 assenti senza diritto. Premi **Salva presenze**.
4. Il riepilogo deve mostrare 35 componenti, 28 presenti aventi diritto e 33 aventi diritto complessivi.
5. Nella console Firebase, sotto **Data**, deve apparire `aula → session`, con i conteggi salvati. Un secondo dispositivo con un account autorizzato alla lettura vede la stessa seduta.

Se compare **Accesso verificato · seduta locale**, il login è riuscito ma il database non è collegato. Controlla che sia attivo e che le regole siano pubblicate, poi esci e accedi nuovamente. Per verificare una scrittura occorre usare la seduta reale: **Demo locale del presidente** non scrive mai su Firebase.

## Come funzionano i conteggi

- **Presenti totali** comprende anche i presenti senza diritto.
- **Assenti totali** comprende anche gli assenti senza diritto.
- **Presenti con diritto** = presenti totali − presenti senza diritto.
- **Componenti con diritto** = presenti + assenti − presenti senza diritto − assenti senza diritto.
- Quorum e maggioranze sono calcolati su questi valori e fissati all’apertura di ogni votazione.
- L’elenco nominativo è facoltativo. Se selezioni **Calcolo dall’elenco nominativo**, i conteggi derivano invece dalle persone registrate.
- In modalità numerica gli account votanti possono votare senza un elenco precompilato; i nomi/email per il voto palese provengono dagli account. Per lo scrutinio manuale non occorre nessun account dei partecipanti.
