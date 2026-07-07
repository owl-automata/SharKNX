# Come Inviare Comandi KNX

SharKNX consente di inviare sia comandi di scrittura che di lettura a qualsiasi indirizzo di gruppo KNX mentre la sessione di monitoraggio è attiva. Questa guida illustra il compositore di comandi (command composer), tutte le scorciatoie dell'interfaccia per aprirlo e come utilizzare i pulsanti rapidi (chip) per ripetere i comandi inviati di frequente.

---

## Prerequisiti

- Un gateway selezionato e la sessione di monitoraggio avviata (vedi [Connettersi a un Gateway](connect-to-gateway.md)).
- Opzionalmente, un progetto ETS caricato in modo che i nomi degli indirizzi di gruppo e i DPT vengano precompilati automaticamente.

---

## Il Compositore di Comandi (Command Composer)

Il compositore di comandi è l'interfaccia principale per l'invio. Presenta quattro campi:

| Campo | Descrizione |
|---|---|
| **Group address** | L'indirizzo di gruppo KNX di destinazione. Digitalo manualmente (es. `1/2/3`) o tocca l'icona di ricerca per sfogliare il tuo progetto ETS caricato |
| **Command type** | **Write (Scrittura)** per inviare un valore, **Read (Lettura)** per richiedere il valore attuale |
| **DPT** | Il tipo e il sottotipo di datapoint (es. DPT 1.001 - Switch/Interruttore). Viene precompilato automaticamente se l'indirizzo viene selezionato dai dati di progetto |
| **Value** | Per i comandi di scrittura: il valore da inviare, presentato tramite un'interfaccia di input adeguata al DPT (interruttore, cursore, selettore colore, campo numerico, ecc.) |

Tocca **Send (Invia)** per trasmettere il comando. Questo apparirà immediatamente nell'elenco dei telegrammi del monitor.

---

## Punti di Accesso all'Interfaccia

### Dalla Pagina Monitor (Metodo Principale)

1. Avvia il monitor - il FAB verde di avvio si trasformerà in un **FAB di invio** rosso.
2. Tocca il **FAB di invio**.
3. Si aprirà una schermata inferiore. Tocca **New command** per aprire il compositore di comandi.
4. Compila i campi e tocca **Send**.

### Pulsanti Rapidi (Quick-Send Chips)

Dopo aver inviato un comando, nella schermata inferiore apparirà un **chip** (pulsante rapido) che mostra l'indirizzo di gruppo e il valore. Questi chip rimangono memorizzati per l'intera sessione.

- **Tocca un chip** per reinviare istantaneamente lo stesso identico comando senza dover riaprire il compositore.
- **Tieni premuto a lungo su un chip** per riaprire il compositore di comandi con l'indirizzo di gruppo e il DPT già precompilati - utile per effettuare un nuovo invio modificando solo il valore.

### Da un Telegramma nell'Elenco del Monitor

1. Tocca una qualsiasi riga di telegramma per aprirne la schermata dei dettagli.
2. Tocca **Write** - il compositore di comandi si aprirà con l'indirizzo di gruppo e il DPT già precompilati in base al telegramma selezionato.
3. Inserisci un valore e tocca **Send**.

La schermata dei dettagli presenta anche un pulsante **Read** che invia immediatamente una richiesta di lettura senza aprire il compositore.

### Dalla Pagina Project - Scheda Group Addresses

1. Vai alla pagina **Project** → scheda **Group Addresses**.
2. Naviga all'interno dell'albero e tocca un singolo indirizzo di gruppo.
3. Nella schermata inferiore, tocca **Write** per aprire il compositore di comandi precompilato con indirizzo e DPT, oppure tocca **Read** per inviare immediatamente un comando di lettura.

### Dalla Pagina Project - Scheda Devices

1. Vai alla pagina **Project** → scheda **Devices**.
2. Espandi un dispositivo e tocca un qualsiasi indirizzo di gruppo elencato sotto di esso.
3. Apparirà la medesima schermata inferiore - tocca **Write** o **Read**.

### Dalla Pagina Communication Objects

1. Vai alla pagina **Project** → scheda **Devices**.
2. Tocca un dispositivo (o tieni premuto a lungo su un dispositivo dotato di indirizzi di gruppo) per aprirne la schermata dei dettagli.
3. Tocca **Communication Objects** per aprire la pagina degli oggetti di comunicazione di quel dispositivo.
4. Tocca un qualsiasi indirizzo di gruppo mostrato sotto un oggetto di comunicazione - apparirà la medesima schermata inferiore di Read/Write, precompilata con indirizzo e DPT.

### Dalla Scheda Inspect - Sezione Associations

Quando hai ricostruito le tabelle di comunicazione di un dispositivo nella scheda **Management → Inspect**, la scheda Associations elenca tutti gli indirizzi di gruppo trovati nella memoria fisica del dispositivo.

1. Tocca un qualsiasi indirizzo di gruppo nella scheda Associations.
2. Poiché il tipo di datapoint (DPT) non è rilevabile dalla sola memoria del dispositivo, verrà mostrato un **campo di input per valori grezzi (raw value input)** anziché un'interfaccia grafica dedicata ai DPT. Inserisci un valore esadecimale o decimale e invia.
3. È inoltre disponibile un pulsante **Read** per inviare una richiesta di lettura a quell'indirizzo.

---

## Inviare un Comando di Lettura (Read)

Una richiesta di lettura comanda al dispositivo che attualmente detiene lo stato di un indirizzo di gruppo di rispondere trasmettendo il suo valore attuale. Il telegramma di risposta apparirà nell'elenco del monitor. Se l'app era già in modalità di monitoraggio nel momento in cui hai toccato **Read** dalla pagina Project, rimarrà in ascolto di una risposta per quell'indirizzo per circa un secondo, mostrando il risultato direttamente all'interno della schermata inferiore.

---

## Note Importanti

- L'invio dei comandi è possibile solo mentre il monitor è in esecuzione. Le schede delle azioni nelle Shark Hunts fanno eccezione - esse gestiscono la connessione e l'invio in modo indipendente per ciascuna hunt.
- Se utilizzi un indirizzo di gruppo protetto tramite KNX Data Secure, l'indirizzo del mittente deve essere configurato prima che le scritture sicure possano essere accettate dal dispositivo. Vedi [Configurare KNX Data Secure](setup-knx-data-secure.md).
- I comandi inviati compaiono nell'elenco del monitor esattamente come qualsiasi altro telegramma, consentendoti di verificare immediatamente se il bus ha risposto con un riscontro (ACK).
