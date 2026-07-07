# Come Ispezionare gli Oggetti di Comunicazione di un Dispositivo

La scheda Inspect nella pagina Management legge le tabelle di comunicazione di un dispositivo direttamente dalla sua memoria e ricostruisce quali oggetti di comunicazione esistono, quali flag possiedono e quali indirizzi di gruppo vi sono collegati - il tutto senza la necessità di un progetto ETS. Questo è il metodo più affidabile per comprendere un dispositivo sconosciuto o non correttamente documentato.

---

## Prerequisiti

- Connessione a un gateway KNX attiva (vedi [Connettersi a un Gateway](connect-to-gateway.md)).
- L'indirizzo individuale del dispositivo che si desidera ispezionare.

---

## Passaggi

1. Vai a **Management → scheda Inspect**.
2. Inserisci l'indirizzo individuale del dispositivo nel campo di input.
   - Puoi raggiungere questa scheda con il campo già precompilato anche dalla scheda **Prog. Mode** (toccando **Comm. Info** su una scheda), dalla scheda di un dispositivo in **Line Scan** (toccando **Rebuild Communication**), o da qualsiasi schermata dei dettagli del dispositivo.
3. Tocca **Read (Leggi)**. Una barra di avanzamento mostrerà l'operazione in corso (tabella degli indirizzi, tabella delle associazioni, oggetti di comunicazione).
4. Apparirà una scheda di sessione relativa al dispositivo. Il colore del bordo indica l'esito positivo (verde) o negativo (rosso).

---

## Lettura delle Informazioni Complete del Dispositivo

La lettura della tabella di comunicazione non include di default le informazioni dettagliate del dispositivo (produttore, firmware, ecc.). Tocca **Read Full Info** sulla scheda di sessione per recuperare separatamente tali dettagli.

---

## Visualizzare i Dettagli della Sessione

Tocca la scheda di sessione per aprire la pagina dei dettagli completi. La barra superiore presenta un pulsante di **ricaricamento (reload)** per eseguire nuovamente la lettura e un pulsante **condividi (share)** per esportare e condividere un report in formato PDF per questa sessione.

La pagina dei dettagli presenta tre schede:

### Associations (Associazioni)

Elenca tutti gli oggetti di comunicazione che hanno almeno un indirizzo di gruppo collegato:

| Colonna | Descrizione |
|---|---|
| Number | Indice dell'oggetto di comunicazione |
| Flags | R Lettura (Read) · W Scrittura (Write) · C Comunicazione · T Trasmissione (Transmit) · U Aggiornamento (Update) · I Lettura all'inizializzazione (Read-on-Init) |
| Size | Dimensione dei dati dell'oggetto (1 bit, 1 byte, 2 byte, ecc.) |
| Group addresses | Indirizzi di gruppo collegati a questo oggetto |

Tocca qualsiasi indirizzo di gruppo per inviare un comando di **Read (Lettura)** o **Write (Scrittura)**. Poiché il tipo di datapoint (DPT) non può essere ricavato dalla sola memoria hardware, viene utilizzato un inserimento di valori in esadecimale grezzo o decimale anziché un'interfaccia grafica dedicata ai DPT.

Utilizza **Export CSV** o **Export TXT** per esportare l'elenco delle associazioni di questa sessione.

### Device Info

Mostra la scheda informativa completa del dispositivo se è stata eseguita l'azione **Read Full Info**. Include un pulsante **Copy All** per copiare tutti i campi negli appunti.

### Addresses

Una tabella di tutti gli indirizzi di gruppo trovati nella tabella degli indirizzi del dispositivo all'interno della memoria (indice, formato a 3 livelli, a 2 livelli, esadecimale). Utilizza **Copy All** o **Export CSV** per estrarre l'elenco completo.

---

## Gestione delle Sessioni

Le sessioni sono **persistenti** - rimangono memorizzate al riavvio dell'applicazione e restano disponibili finché non deciderai di svuotarle.

- **Clear** (sopra l'elenco delle schede) - rimuove tutte le sessioni.
- **Export** (sopra l'elenco delle schede) - esporta tutte le sessioni insieme in un unico file PDF.
- **Share** (nella barra superiore della pagina dei dettagli di una sessione) - esporta e condivide esclusivamente quella singola sessione in formato PDF.

---

## Note Importanti

- Una lettura fallita (bordo rosso) indica solitamente che il dispositivo non risponde, si trova in uno stato di errore o l'indirizzo inserito è errato. Utilizza la funzione **Check** dalla scheda Devices per verificare prima che il dispositivo sia effettivamente presente sul bus.
- Se il dispositivo richiede le chiavi di diagnostica (tool keys) di KNX Data Secure per le operazioni di gestione del dispositivo, carica il file `.knxkeys` nella scheda **Discovery → Security** prima di avviare la lettura.
