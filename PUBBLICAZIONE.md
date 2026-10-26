# Pubblicazione su GitHub Pages

## Contenuto

- `dist/index.html`: pagina principale.
- `dist/style.css`: interfaccia e stampa PDF.
- `dist/app.js`: presidenza, votazioni, verbale e tabellone.
- `dist/firebase-config.js`: configurazione web pubblica Firebase fornita da Jacopo.
- `.github/workflows/pages.yml`: pubblicazione automatica della cartella `dist`.

Non serve un server applicativo né installare dipendenze. Font e SDK Firebase vengono caricati da servizi esterni. Il pacchetto non contiene password, token GitHub, credenziali di servizio, dati delle sedute o metadati dell’hosting precedente.

## Repository e primo deploy

1. Crea un repository, ad esempio `assemblea-seborg`, con branch principale `main`.
2. Carica il contenuto di questa cartella mantenendo anche `.github/workflows/pages.yml`.
3. In **Settings → Pages → Build and deployment → Source**, seleziona **GitHub Actions**.
4. In **Actions**, avvia **Pubblica Assemblea Parlamentare → Run workflow**, oppure esegui un nuovo push su `main`.
5. Il collegamento pubblicato apparirà in **Settings → Pages** e nel deployment dell’azione.

Con GitHub Free, GitHub Pages richiede un repository pubblico. Le disponibilità per repository privati dipendono dal piano GitHub.

## Dominio personalizzato

Il nome del dominio non è ancora stato scelto né configurato.

1. In **Settings → Pages → Custom domain**, inserisci il dominio desiderato (ad esempio `parlamento.ferrioli.eu`, solo come proposta).
2. Per un sottodominio, configura presso il gestore DNS un record **CNAME** verso `<account-github>.github.io`, usando il nome effettivo dell’account che possiede il repository. Non includere il nome del repository nel valore DNS.
3. Attendi la verifica DNS e l’emissione del certificato, poi abilita **Enforce HTTPS**.
4. In Firebase Authentication, aggiorna **Settings → Authorized domains** con l’host GitHub Pages effettivo e il dominio personalizzato, se usati per i flussi di autenticazione.

Per un dominio principale senza sottodominio, segui le istruzioni GitHub ufficiali sui record DNS apex. Non cambiare record esistenti di posta o di altri siti. Un file CNAME nel codice non sostituisce la configurazione del dominio nelle impostazioni Pages.

## Dati e login

Gli account Firebase esistenti determinano i ruoli. Il 26 ottobre 2026 il database del progetto `ferriolieu` rispondeva che era disattivato. Dopo un login riuscito l’app può proseguire in locale; per sincronizzare computer diversi occorre riattivare Realtime Database.

Il sito GitHub Pages non eredita l’accesso privato dell’hosting precedente. La modalità demo rimane disponibile come richiesto per il testing.

Il salvataggio locale è legato all’indirizzo del sito: i dati salvati sul precedente hosting non migrano automaticamente su GitHub Pages o su un nuovo dominio. Prima del passaggio salva i verbali che vuoi conservare.

Il pulsante **Apri tabellone** funziona sul nuovo hosting senza cambiare il codice e mantiene la regia nella scheda originale. Le due schede devono usare lo stesso browser/profilo e lo stesso indirizzo del sito.

## Fonti ufficiali

- https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages
- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
