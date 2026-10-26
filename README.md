# Assemblea Parlamentare Stato di Seborg - FERRIOLI.EU

Applicazione web statica per gestire sedute, interventi, mozioni, votazioni e verbali.

## Accesso

Accesso esclusivamente tramite Firebase Email/Password. Il presidente è `jacopo@ferrioli.eu`; i segretari sono `amministrazione.generale@cas.ferrioli.eu` e `amministrazione@ferrioli.eu`. Gli altri account sono votanti.

La pagina di accesso non offre demo né modifica della configurazione Firebase. La demo è disponibile soltanto dopo il login del presidente, in **Impostazioni → Demo locale del presidente**. Usa dati separati dalla seduta reale e non scrive sul database. **Torna alla seduta reale** ripristina il lavoro precedente.

## Partecipanti

La modalità principale consente al presidente di inserire presenti totali, assenti totali, presenti senza diritto e assenti senza diritto, senza nomi. Totali e aventi diritto sono calcolati automaticamente. L’elenco nominativo rimane disponibile come opzione secondaria; selezionando la relativa fonte, il conteggio deriva dall’elenco. Le sedute preesistenti con membri mantengono la modalità nominativa finché il presidente non la cambia.

Quorum, maggioranze e controllo del totale dei voti usano la fonte selezionata. Le presenze sono fissate all’apertura di ogni votazione, così una modifica successiva non cambia il risultato storico.

In modalità numerica, i votanti autenticati possono esprimersi senza un elenco precompilato. Il voto palese usa nome/email dell’account. Il sistema resta una simulazione con controlli semplici.

## Altre funzioni

- Ordine del giorno, apertura, sospensione e ripresa della seduta.
- Interventi per numero del posto, coda, timer con pausa, aggiunta di tempo e sforamento.
- Mozioni ed emendamenti, voto manuale o dai dispositivi, palese o segreto.
- Scrutinio riservato e pubblicazione dei risultati.
- Tabellone in una scheda separata nello stesso browser/profilo, sincronizzato con la regia.
- Verbale stampabile in PDF tramite la stampa del browser.

## Guide

- [Configurare Firebase e Realtime Database](GUIDA-FIREBASE.md)
- [Modificare i testi su GitHub](MODIFICARE-TESTI.md)
- [Pubblicazione e dominio](PUBBLICAZIONE.md)

I file del sito sono in `dist`. Non serve una build: GitHub Actions pubblica questa cartella. La configurazione web Firebase è in `dist/firebase-config.js`; Analytics non viene inizializzato.

## Verifiche

Esegui `node tests/assembly.test.cjs`. Il test verifica accesso, permessi della demo, separazione tra demo e seduta reale, conteggi numerici/nominativi, validazione, quorum, snapshot delle presenze, voto digitale e dati del tabellone.
