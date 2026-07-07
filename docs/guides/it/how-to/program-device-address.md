# Come Programmare l'Indirizzo Individuale di un Dispositivo

SharKNX consente di programmare (scrivere) un indirizzo individuale KNX in un dispositivo direttamente dal tuo smartphone o PC - senza la necessità di utilizzare ETS o di avere un computer fisicamente collegato in cantiere. Sono disponibili due metodi: tramite il pulsante di programmazione fisico o tramite il numero di serie del dispositivo (senza premere alcun pulsante).

---

## Prerequisiti

- Connessione a un gateway KNX attiva (vedi [Connettersi a un Gateway](connect-to-gateway.md)).
- Il nuovo indirizzo individuale che si desidera assegnare, ricavato dal progetto o inserito manualmente.

---

## Metodo A - Tramite il Pulsante di Programmazione

Utilizza questo metodo quando hai accesso fisico al dispositivo (o se un collega in cantiere può premere il pulsante per te).

1. Vai a **Management → scheda Line Scan**.
2. Esegui una scansione della linea nell'area interessata (vedi [Scansionare una Linea Bus](scan-bus-line.md)), quindi tocca la scheda del dispositivo che desideri riprogrammare per aprirne la schermata dei dettagli.
   - In alternativa, vai a **Management → scheda Devices**, inserisci l'indirizzo individuale corrente del dispositivo e utilizza le azioni disponibili da lì.
3. Nella schermata dei dettagli del dispositivo, tocca **Program Address**.
4. Inserisci il nuovo indirizzo individuale nel campo di input, oppure tocca l'**icona di ricerca** per selezionarne uno dal progetto ETS caricato.
5. Tocca **Program via programming button**.
6. L'applicazione attenderà fino a **20 secondi** che un dispositivo entri in modalità di programmazione. Premi il pulsante di programmazione sul dispositivo fisico entro questa finestra temporale.
7. Quando l'app rileva un dispositivo in modalità di programmazione, scrive il nuovo indirizzo e conferma l'esito positivo dell'operazione.

> L'applicazione verifica se il nuovo indirizzo sia già utilizzato da un altro dispositivo sull'impianto reale. Se viene rilevato un conflitto, verrai avvertito prima che la scrittura venga effettivamente eseguita.

---

## Metodo B - Tramite Numero di Serie

Utilizza questo metodo quando disponi già del numero di serie del dispositivo, ottenuto da una precedente operazione di **Read Info**. Non è richiesta la pressione fisica del pulsante - una soluzione ideale per dispositivi installati in posizioni difficili da raggiungere.

1. Assicurati innanzitutto che il numero di serie del dispositivo sia noto: esegui un'operazione di **Read Info** dalla scheda del dispositivo in Line Scan o dalla scheda Devices, se non lo hai già fatto.
2. Nella schermata dei dettagli del dispositivo o nella scheda Devices, tocca **Program Address**.
3. Inserisci il nuovo indirizzo individuale o selezionalo dal progetto.
4. Tocca **Program via serial number**.
5. L'applicazione si rivolgerà direttamente al dispositivo utilizzando il suo numero di serie e scriverà il nuovo indirizzo senza richiedere la pressione del pulsante di programmazione.

---

## Suggerimento - Attivazione Remota della Modalità di Programmazione

Se non riesci a raggiungere fisicamente il pulsante di programmazione, utilizza la funzione **Toggle Programming Mode** dalla scheda del dispositivo o dalla scheda Devices per attivarla prima da remoto. Successivamente, esegui immediatamente **Program via programming button** - l'applicazione rileverà lo stato entro la finestra di 20 secondi. Ricordati di disattivarla nuovamente al termine.

---

## Note Importanti

- Dopo la programmazione, verifica il risultato toccando **Check** sulla scheda del dispositivo per confermare che il nuovo indirizzo sia effettivamente attivo sul bus.
- Questo flusso di lavoro supporta le fasi di messa in servizio iniziale (commissioning): scansione della linea → identificazione di tutti i dispositivi → programmazione degli indirizzi → connessione e download dei programmi da ETS.
