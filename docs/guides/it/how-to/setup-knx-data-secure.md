# Come Configurare KNX Data Secure

KNX Data Secure cifra i singoli telegrammi KNX al livello applicazione (application layer). Per ricevere e inviare correttamente i telegrammi protetti, SharKNX necessita delle chiavi di gruppo del tuo progetto ETS e, per l'invio, di un indirizzo mittente configurato. Questa guida illustra entrambi i passaggi.

Per comprendere i concetti di base sul funzionamento di KNX Data Secure, vedi [KNX Data Secure](../concepts/knx-data-secure.md).

---

## Prerequisiti

- Un file di progetto ETS `.knxproj` che includa indirizzi di gruppo KNX Data Secure.
- Un indirizzo individuale KNX che SharKNX possa utilizzare come propria identità mittente. Questo indirizzo deve esistere nel progetto ETS e disporre dei diritti di accesso per gli indirizzi di gruppo a cui intendi trasmettere.

> **Vincolo KNX IP Secure:** L'invio in modalità KNX Data Secure richiede che il monitor sia in esecuzione tramite un tunnel KNX IP Secure. Se il tuo gateway non supporta KNX IP Secure, esistono due soluzioni alternative ("workaround") applicabili in ETS - consulta la pagina concettuale di [KNX Data Secure](../concepts/knx-data-secure.md#sending-constraints) per tutti i dettagli.

---

## Parte 1 - Caricare le Chiavi di Gruppo

Le chiavi di gruppo sono incorporate all'interno del file `.knxproj`. È sufficiente caricare il progetto - SharKNX estrarrà le chiavi in modo completamente automatico.

1. Vai alla pagina **Project**.
2. Tocca il **FAB della cartella** per aprire il selettore di file, oppure seleziona un progetto caricato di recente dall'elenco della cronologia.
3. Seleziona il tuo file `.knxproj`.
   - Se il progetto è protetto da password, inserisci la password quando richiesto.
4. Una volta completato il caricamento, verifica la presenza del **banner Data Secure** nella parte superiore della pagina Project. Se appare, significa che il progetto contiene indirizzi di gruppo Data Secure e che le relative chiavi sono state caricate con successo.

---

## Parte 2 - Configurare l'Indirizzo Mittente

SharKNX deve sapere quale indirizzo individuale KNX utilizzare durante l'invio di telegrammi Data Secure. Senza questa informazione, gli invii protetti falliranno.

1. Dalla pagina **Project**, tocca il **banner Data Secure**. Questo aprirà la schermata di configurazione del mittente.
   - In alternativa, naviga in **Project → scheda Devices**, individua il dispositivo il cui indirizzo desideri utilizzare come mittente e accedi alla configurazione del mittente da lì.
2. Nella schermata di configurazione del mittente, scegli uno dei due approcci disponibili:

### Opzione A - Configurare uno specifico indirizzo individuale

1. Tocca **Add sender address**.
2. Inserisci l'indirizzo individuale (es. `1.1.250`), oppure tocca l'icona di ricerca per selezionare un dispositivo dal progetto caricato.
3. Conferma. L'indirizzo verrà salvato come mittente attendibile.

### Opzione B - Utilizzare l'indirizzo mittente globale (automatico)

Se preferisci non specificare manualmente i singoli indirizzi:

1. Tocca **Set global sender address**.
2. Inserisci l'indirizzo da utilizzare per tutti gli invii protetti.

SharKNX utilizzerà questo indirizzo per qualsiasi indirizzo di gruppo Data Secure che non abbia uno specifico indirizzo mittente configurato.

> Se nessuna delle due opzioni presenta un indirizzo incluso nell'elenco dei mittenti attendibili del progetto ETS per un determinato indirizzo di gruppo, il dispositivo ricevente rifiuterà il telegramma. Assicurati che l'indirizzo configurato sia stato aggiunto all'elenco dei mittenti dell'oggetto di gruppo in ETS.

---

## Parte 3 - Verifica

1. Avvia il monitor (connettiti al tuo gateway e tocca il FAB di avvio nella pagina Monitor).
2. Attiva un telegramma Data Secure sul bus - ad esempio, premendo un pulsante a parete.
3. Il telegramma dovrebbe apparire nell'elenco del monitor con il suo valore decodificato (e non solo come dato grezzo). Questo conferma che la chiave di gruppo è stata applicata correttamente.
4. Per verificare l'invio: dal monitor, tieni premuto a lungo sulla riga di un telegramma con indirizzo di gruppo Data Secure per aprire il compositore di comandi precompilato con indirizzo e DPT. Invia un comando di scrittura. Il dispositivo dovrebbe rispondere come previsto.

---

## Note Importanti

- Le chiavi di gruppo vengono rilette ogni volta che carichi un progetto. Se le chiavi in ETS sono state cambiate (ad esempio dopo una nuova messa in servizio), ricarica il file di progetto per acquisire le chiavi aggiornate.
- Gli indirizzi dei mittenti rimangono memorizzati anche al riavvio dell'applicazione. È necessario configurarli una sola volta per progetto.
- Il badge Data Secure presente nella pagina Monitor e nelle pagine delle Shark Hunt mostra a colpo d'occhio lo stato attuale del mittente - il colore ambra indica che i mittenti non sono ancora stati configurati, il verde indica che il sistema è pronto.
