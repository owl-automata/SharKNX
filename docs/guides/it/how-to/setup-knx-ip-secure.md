# Come Configurare KNX IP Secure

KNX IP Secure cifra la connessione tramite tunnel tra SharKNX e il tuo gateway utilizzando l'algoritmo AES-128 CCM su protocollo TCP. Prima che SharKNX possa connettersi a un gateway sicuro, necessita delle credenziali corrispondenti. Questa guida spiega come caricarle.

Per comprendere i concetti di base su cosa protegga KNX IP Secure e su come funzioni, vedi [KNX IP Secure](../concepts/knx-ip-secure.md).

---

## Cosa ti Serve

Una delle seguenti sorgenti di credenziali (tutte generate da ETS):

| Formato | Come ottenerlo |
|---|---|
| File del keystore `.knxkeys` | Esporta da ETS: Progetto → Sicurezza → Esporta archivio chiavi (Export keystore) |
| File di progetto ETS `.knxproj` | Lo stesso file di progetto utilizzato per caricare gli indirizzi di gruppo; contiene già le credenziali dei dispositivi |
| Chiave di dorsale / Backbone key (stringa esadecimale) | Reperibile in ETS sotto le impostazioni IP Secure dell'interfaccia interessata |

---

## Passaggio 1 - Aprire la Scheda Security

1. Vai alla pagina **Discovery**.
2. Tocca la scheda **Security**.

---

## Passaggio 2 - Caricare le Credenziali

Sono disponibili tre metodi. Utilizza quello che corrisponde alla sorgente in tuo possesso:

### Metodo A - Caricare un file del keystore `.knxkeys`

1. Tocca **Load .knxkeys file**.
2. Seleziona il file `.knxkeys` dalla memoria del tuo dispositivo.
   - Se il file è protetto da password, inserisci la password del keystore quando richiesto.
3. Apparirà una scheda di riepilogo che conferma quante credenziali di interfaccia sono state caricate.

### Metodo B - Caricare le credenziali da un file di progetto ETS

Se hai già un file `.knxproj` caricato o disponibile:

1. Tocca **Load from ETS project**.
2. Seleziona il file `.knxproj` (o conferma il progetto già attualmente caricato).
   - Se il progetto è protetto da password, inserisci la password del progetto quando richiesto.
3. Le credenziali verranno estratte dal file di progetto e caricate in modo del tutto automatico.

### Metodo C - Inserire manualmente una chiave di dorsale (backbone key)

1. Tocca **Enter backbone key**.
2. Incolla o digita la chiave di dorsale esadecimale a 32 caratteri.
3. Conferma. La chiave verrà salvata e sarà utilizzata per qualsiasi gateway che la richieda.

---

## Passaggio 3 - Verificare la Scheda del Gateway

1. Vai alla scheda **Discover** ed esegui una scansione dei gateway, oppure apri la scheda **Config** se il tuo gateway è già stato salvato in precedenza.
2. Individua il tuo gateway sicuro. La sua scheda dovrebbe mostrare l'**icona di un lucchetto** ad indicare che KNX IP Secure è supportato.
3. Se le credenziali sono state caricate con successo, l'icona del lucchetto apparirà piena/attiva. Se l'icona è vuota o la scheda del gateway mostra un avviso relativo alle credenziali, ripeti il Passaggio 2 utilizzando il file corretto.

---

## Passaggio 4 - Connettersi

1. Tocca **Select** sulla scheda del gateway per impostarlo come gateway attivo.
2. Avvia il monitor (o connettiti dalla pagina di una shark hunt). SharKNX utilizzerà automaticamente il tunnel sicuro TCP.
3. Se la connessione va a buon fine, il badge di connessione diventa verde e i telegrammi inizieranno a scorrere normalmente.

Se la connessione fallisce restituendo un errore di sicurezza, le cause più comuni sono:
- File keystore errato (credenziali destinate a un altro gateway).
- Password del keystore o del progetto errata.
- La chiave di configurazione (tool key) del gateway è stata cambiata in ETS dopo l'esportazione del keystore - esporta nuovamente il keystore da ETS e ricaricalo nell'app.

---

## Note Importanti

- Le credenziali caricate tramite file `.knxkeys` o `.knxproj` vengono memorizzate sul dispositivo e rimangono attive anche al riavvio dell'applicazione. Non è necessario caricarle nuovamente a ogni sessione.
- Se un file `.knxkeys` contiene le chiavi di diagnostica (tool keys) per i singoli dispositivi (utilizzate per le operazioni di gestione dei dispositivi), anch'esse verranno caricate in questa fase e saranno disponibili nelle pagine Management e Project.
- Nella scheda Security è possibile visualizzare la cronologia dei file di credenziali caricati in precedenza.
- Per utilizzare un keystore differente, è sufficiente caricare il nuovo file - questo andrà a sostituire integralmente le credenziali precedenti.
