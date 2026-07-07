# Pagina Management (Gestione)

La pagina Management è focalizzata sulla diagnostica dei dispositivi e dell'installazione KNX. È suddivisa in quattro schede: **Prog. Mode**, **Devices**, **Line Scan** e **Inspect**.

---

## Scheda Prog. Mode

Questa scheda consente di scansionare il bus alla ricerca di dispositivi che hanno la modalità di programmazione attiva in quel momento.

Tocca il **FAB radar** (pulsante fluttuante) per avviare la scansione. L'applicazione rimane in ascolto dei dispositivi in modalità di programmazione e li elenca sotto forma di schede. La durata della scansione e l'intervallo di ping sono configurabili nelle **Impostazioni Scansione** (icona ingranaggio → Impostazioni Scansione).

Ogni scheda relativa a un dispositivo rilevato presenta due pulsanti:

- **Check Info** - naviga verso la scheda Devices precompilando l'indirizzo individuale del dispositivo rilevato, pronto per la lettura delle informazioni del dispositivo.
- **Comm. Info** - naviga verso la scheda Inspect precompilando l'indirizzo, pronto per la lettura delle tabelle di comunicazione del dispositivo.

Questo approccio consente di effettuare prima una scansione rapida, per poi passare immediatamente a una diagnostica più approfondita su qualsiasi dispositivo trovato in modalità di programmazione.

---

## Scheda Devices

La scheda Devices consente di eseguire azioni diagnostiche su qualsiasi indirizzo individuale di un dispositivo - sia esso rilevato tramite scansione o cercato direttamente.

### Badge Data Secure

Nella parte superiore della scheda, un badge indica se le chiavi dei dispositivi KNX Data Secure sono state caricate (da un file `.knxkeys` nella scheda Security della pagina Discovery). Se non è presente alcuna chiave, il badge è di colore ambra. Se le chiavi sono caricate, il badge diventa blu e mostra il conteggio dei dispositivi sicuri. Toccando il badge si apre una schermata con i dettagli e una scorciatoia per caricare un file `.knxkeys`.

### Inserimento Indirizzo

Inserisci un indirizzo individuale KNX nel campo di input. Tocca l'**icona di ricerca** per sfogliare i dispositivi dal tuo progetto ETS caricato e selezionarne uno direttamente.

### Azioni

Una volta inserito un indirizzo, sono disponibili quattro azioni:

| Azione | Descrizione |
|---|---|
| **Check** | Verifica se il dispositivo è presente e risponde sul bus |
| **Read Info** | Legge le informazioni dettagliate direttamente dal dispositivo |
| **Toggle Programming Mode** | Attiva o disattiva da remoto la modalità di programmazione del dispositivo |
| **Restart** | Invia un comando di riavvio (restart) al dispositivo |

L'azione **Read Info** recupera i seguenti campi dal dispositivo:
- Descrittore del dispositivo (es. System B)
- Stato della modalità di programmazione
- Produttore e codice d'ordine
- Versione del firmware
- Stato di caricamento (load state) e stato di esecuzione (run state)
- Versione dell'applicazione
- Stato della tabella degli indirizzi e delle associazioni
- Lunghezza massima APDU
- Tipo di hardware
- Flag di errore e stato del dispositivo

---

## Scheda Line Scan (Scansione Linea)

La scheda Line Scan esegue una scansione di una linea bus KNX per individuare tutti i dispositivi fisicamente presenti su di essa, indipendentemente dal contenuto del tuo progetto ETS. Questa funzione è estremamente utile per verificare un'installazione, rilevare dispositivi imprevisti o lavorare su un progetto sconosciuto.

### Scheda Impostazioni Scansione

Configura la scansione prima di iniziare:

| Impostazione | Descrizione |
|---|---|
| Area e linea | L'indirizzo `area.linea` KNX da scansionare (es. `1.1`). Utilizza **Choose from project** per selezionare una linea dal tuo progetto ETS caricato - questa opzione seleziona automaticamente anche il tipo di mezzo corretto. |
| Tipo di mezzo | TP, IP o IoT. Necessario all'applicazione per conoscere l'intervallo di indirizzi dei dispositivi da sondare. |
| Intervallo (Range) | Indirizzo iniziale e finale all'interno della linea (0–255). Stringi l'intervallo per velocizzare la scansione o per verificare un segmento specifico. |

Tocca il **FAB di scansione** per iniziare. La scansione può essere interrotta in qualsiasi momento prima del completamento.

### Risultati della Scansione

I dispositivi rilevati appaiono sotto forma di schede. Il colore del bordo della scheda indica la tipologia di dispositivo:

| Colore | Tipo di dispositivo |
|---|---|
| Blu | Accoppiatore KNX (Coupler) |
| Rosso | Dispositivo di applicazione standard |
| Verde | Dispositivo KNX Secure |

Al termine della scansione, sopra l'elenco delle schede appare il pulsante **Read Device Info**. Toccandolo, l'app legge in sequenza le informazioni di tutti i dispositivi rilevati (produttore, numero di serie e altri dettagli) - ideale per ricostruire rapidamente il quadro di un impianto non configurato da te.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-line-scan.png" width="320" alt="Scheda Line Scan che mostra le schede dei dispositivi rilevati con bordi codificati per colore e il pulsante Read Device Info" />
</div>

### Schermata dei Dettagli della Scheda Dispositivo

Tocca la scheda di qualsiasi dispositivo rilevato per aprire la sua schermata dei dettagli, che contiene:

- Una scheda informativa del dispositivo (popolata se è stato eseguito Read Device Info)
- Le stesse quattro azioni diagnostiche della scheda Devices: **Check**, **Read Info**, **Toggle Programming Mode**, **Restart**
- **Program Address** - apre una sotto-pagina in cui è possibile inserire un nuovo indirizzo individuale (o cercarne uno nel progetto) e programmarlo nel dispositivo utilizzando uno dei due metodi seguenti:
  - **Via programming button** - attende fino a 20 secondi che il dispositivo entri in modalità di programmazione, quindi scrive l'indirizzo. Verifica inoltre la presenza di conflitti di indirizzo rispetto all'installazione reale.
  - **Via serial number** - se hai già letto le info del dispositivo e possiedi il suo numero di serie, programma l'indirizzo senza richiedere l'accesso fisico al pulsante di programmazione.
- **Rebuild Communication** - naviga verso la scheda Inspect precompilando l'indirizzo di questo dispositivo.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-device-card.png" width="320" alt="Schermata dei dettagli della scheda dispositivo in Line Scan che mostra i pulsanti delle azioni diagnostiche e l'opzione Program Address" />
</div>

---

## Scheda Inspect (Ispeziona)

La scheda Inspect legge le tabelle di comunicazione di un dispositivo direttamente dalla sua memoria. Questa operazione ricostruisce quali oggetti di comunicazione esistono, quali flag possiedono e quali indirizzi di gruppo sono ad essi collegati - il tutto senza la necessità di avere un progetto ETS. È il metodo più efficace per comprendere un dispositivo sconosciuto o verificare un componente in un progetto creato da terzi.

### Lettura di un Dispositivo

Inserisci l'indirizzo individuale di un dispositivo nel campo di input e tocca **Read**. Una barra di avanzamento mostrerà l'operazione in corso. Al termine, apparirà una scheda di sessione per il dispositivo.

Il colore del bordo della scheda indica l'esito positivo o negativo dell'operazione. Ogni scheda mostra:
- Indirizzo individuale del dispositivo
- Descrittore del dispositivo (es. System B, accoppiatore KNX)
- Stato della lettura completa delle info (mostra produttore e codice d'ordine se completata)

Il pulsante **Read Full Info** presente su ciascuna scheda avvia una lettura separata delle informazioni del dispositivo, utile se desideri i dettagli completi senza rallentare la ricostruzione iniziale delle tabelle.

Le schede di sessione sono **persistenti** - rimangono memorizzate anche dopo il riavvio dell'applicazione. Utilizza il pulsante **Clear** sopra l'elenco delle schede per rimuovere tutte le sessioni quando hai finito.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-inspect.png" width="320" alt="Scheda Inspect che mostra molteplici schede di sessione per diversi dispositivi" />
</div>

### Pagina dei Dettagli della Sessione

Tocca qualsiasi scheda di sessione per aprire la sua pagina dei dettagli completi. La barra superiore mostra l'indirizzo e il descrittore del dispositivo, un pulsante di **ricarica** per eseguire nuovamente la ricostruzione e un pulsante di **condivisione** per esportare e condividere un report PDF di questa sessione.

La pagina dei dettagli è suddivisa in tre schede:

#### Associations (Associazioni)

Elenca tutti gli oggetti di comunicazione letti dalla memoria del dispositivo che presentano indirizzi di gruppo collegati:

| Colonna | Descrizione |
|---|---|
| Number | Indice dell'oggetto di comunicazione |
| Flags | R (Lettura), W (Scrittura), C (Comunicazione), T (Trasmissione), U (Aggiornamento), I (Lettura all'inizializzazione) |
| Size | Dimensione dell'oggetto (1 bit, 1 byte, 2 byte, ecc.) |
| Group addresses | Indirizzi di gruppo collegati a questo oggetto |

Ogni indirizzo di gruppo è interattivo. Poiché il tipo di datapoint (DPT) non può essere dedotto esclusivamente dalla memoria, viene presentato un campo di inserimento del valore in formato esadecimale grezzo o decimale per l'invio di comandi di test.

I pulsanti **Export CSV** e **Export TXT** consentono di esportare l'elenco delle associazioni esclusivamente per questo dispositivo.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/management/management-inspect-associations.png" width="320" alt="Scheda Associations che mostra gli oggetti di comunicazione con flag, dimensione e indirizzi di gruppo collegati" />
</div>

#### Device Info

Mostra la scheda informativa completa del dispositivo (i medesimi campi dell'azione Read Info nella scheda Devices). Include un pulsante **Read Info** se non ancora letta, e un pulsante **Copy All** che copia tutti i campi negli appunti per una rapida condivisione con i colleghi.

#### Addresses

Una tabella di tutti gli indirizzi di gruppo letti dalla tabella degli indirizzi del dispositivo in memoria, con colonne dedicate per indice, formato a 3 livelli, formato a 2 livelli e valore esadecimale. Ogni riga è copiabile singolarmente. Sopra la tabella sono disponibili i pulsanti **Copy All** ed **Export CSV**.

---

## Menu di Ottimizzazione (Tune Menu)

L'icona delle regolazioni nella barra superiore fornisce due azioni di esportazione dedicate all'ultimo risultato della scansione di linea:

- **Export as text** - esporta un report TXT contenente il timestamp della scansione, il gateway utilizzato, l'area/linea scansionata, il mezzo trasmissivo e l'elenco dei dispositivi rilevati con le relative info.
- **Export as PDF** - esporta i medesimi contenuti in formato PDF.
