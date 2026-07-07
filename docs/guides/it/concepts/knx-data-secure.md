# KNX Data Secure

KNX Data Secure è l'estensione di sicurezza a livello applicativo dello standard KNX. Cifra e autentica i singoli telegrammi KNX sul mezzo trasmissivo del bus (TP o RF), proteggendoli dall'intercettazione e dalla manipolazione indipendentemente da come vengono trasportati verso la rete IP.

> Questa pagina spiega cos'è KNX Data Secure e come viene gestito da SharKNX. Per la procedura di configurazione dettagliata passo dopo passo, consulta la guida [Configurare KNX Data Secure](../how-to/setup-knx-data-secure.md).

---

## Cosa Protegge KNX Data Secure

I telegrammi KNX standard trasmessi su doppino intrecciato (TP - Twisted Pair) sono leggibili da qualsiasi dispositivo presente sullo stesso segmento di bus. KNX Data Secure risolve questo problema cifrando i dati applicativi di telegrammi di gruppo selezionati tramite l'algoritmo **AES-128 CCM**, lo stesso utilizzato da KNX IP Secure. Ogni telegramma cifrato contiene inoltre un **Message Authentication Code (MAC)** e un **numero di sequenza** incrementale, che insieme prevengono:

- Intercettazione (Eavesdropping) - il payload del telegramma non può essere letto senza la relativa chiave di gruppo.
- Manomissione (Tampering) - qualsiasi modifica al payload rende non valido il MAC.
- Attacchi di tipo "Replay" - un telegramma catturato non può essere inviato nuovamente poiché il suo numero di sequenza risulterebbe fuori ordine.

KNX Data Secure opera a livello applicativo KNX, all'interno del telegramma stesso. È indipendente dal percorso di trasporto - un telegramma protetto da Data Secure è sicuro sia che viaggi su TP, RF o attraverso un tunnel KNXnet/IP.

---

## Chiavi di Gruppo e Lista dei Mittenti

Ogni indirizzo di gruppo KNX Data Secure ha la propria **chiave di gruppo**. La chiave viene utilizzata sia per cifrare il payload sia per calcolare il MAC. Essa viene memorizzata nel portachiavi (keyring) del progetto ETS e distribuita a tutti i dispositivi collegati a quell'indirizzo di gruppo durante la fase di messa in servizio (commissioning).

Oltre alla cifratura, i dispositivi KNX Data Secure mantengono una **lista dei mittenti attendibili** (trusted sender list) per ciascun indirizzo di gruppo: un insieme di indirizzi individuali i cui telegrammi verranno accettati dal dispositivo. I telegrammi provenienti da un indirizzo individuale non presente in questa lista vengono scartati silenziosamente, anche se la cifratura è corretta. Ciò significa che:

- Per **ricevere** correttamente i telegrammi Data Secure, è necessaria la chiave di gruppo.
- Per **inviare** comandi Data Secure che un dispositivo possa effettivamente eseguire, il tuo indirizzo individuale deve essere presente nella lista dei mittenti attendibili del dispositivo per quel determinato indirizzo di gruppo.

---

## Ricezione di Telegrammi Data Secure in SharKNX

SharKNX estrae automaticamente tutte le chiavi di gruppo Data Secure quando viene caricato un file `.knxproj`. Non è richiesta alcuna configurazione separata delle credenziali per il monitoraggio. Una volta caricato un progetto:

- I telegrammi Data Secure in entrata nel Monitor vengono decrittografati in modo trasparente e mostrati con il loro valore decodificato, il nome e il tipo di datapoint (DPT) - esattamente come i telegrammi non protetti.
- Se non è caricato alcun progetto, i telegrammi Data Secure appaiono come esadecimale grezzo (hex) senza valore decodificato (il payload è cifrato e illeggibile senza la chiave).

Il **badge Data Secure** nella riga dei badge della pagina Monitor riflette lo stato corrente: grigio se nel progetto caricato non sono presenti indirizzi di gruppo Data Secure, ambra se gli indirizzi Data Secure sono caricati ma i mittenti non sono stati configurati, e verde quando i mittenti sono configurati e l'invio è pronto.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-data-secure/knx-data-secure-project-banner.png" width="320" alt="Pagina Project con il banner Data Secure che richiede la configurazione del mittente dopo il caricamento di un progetto con indirizzi di gruppo Data Secure" />
</div>

---

## Invio di Telegrammi Data Secure - l'Indirizzo Mittente

Quando SharKNX invia un comando Data Secure, deve presentare un indirizzo individuale che il dispositivo di destinazione riconosca come mittente attendibile. Se l'indirizzo non è presente nella lista dei mittenti del dispositivo, il comando viene ignorato.

SharKNX gestisce questo aspetto tramite la configurazione dei **Data Secure Senders** (Mittenti Data Secure), accessibile dal banner che appare nella pagina Project quando viene caricato un progetto contenente indirizzi di gruppo Data Secure.

Nella pagina dei mittenti è possibile:

- Impostare un **indirizzo mittente globale** - utilizzato per qualsiasi indirizzo di gruppo Data Secure che non ha un indirizzo specifico configurato.
- Impostare **eccezioni per singolo indirizzo** (per-address overrides) - mappare singoli indirizzi di gruppo a specifici indirizzi individuali mittente.
- **Generare automaticamente dai dati di progetto** - SharKNX legge il progetto ETS e crea automaticamente le associazioni indirizzo di gruppo ↔ indirizzo individuale in base ai dispositivi che risultano collegati a ciascun indirizzo di gruppo protetto. Questo è il metodo più rapido per configurare i mittenti quando si dispone di un progetto completo.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-data-secure/knx-data-secure-senders.png" width="320" alt="Pagina di configurazione dei Data Secure Senders che mostra il mittente globale e la lista delle associazioni per singolo indirizzo" />
</div>

---

## Il Vincolo dell'Indirizzo Mittente con KNX IP Secure

Quando SharKNX è connesso tramite un **tunnel KNX IP Secure**, l'indirizzo individuale utilizzato in tutti i telegrammi in uscita viene fissato dal gateway sul valore dell'indirizzo dell'interfaccia di connessione del tunneling. SharKNX non può sovrascrivere questo indirizzo - si tratta di una proprietà nativa del protocollo KNX IP Secure.

Ciò comporta un vincolo pratico: affinché un dispositivo Data Secure accetti i comandi da SharKNX su un tunnel KNX IP Secure, l'indirizzo dell'interfaccia di tunneling deve essere già presente nella lista dei mittenti attendibili del dispositivo all'interno di ETS.

Due approcci funzionano bene nella pratica:

1. **Utilizzare un'interfaccia fittizia (dummy) dedicata in ETS.** Crea un dispositivo di interfaccia virtuale protetto nel tuo progetto ETS e collega ad esso tutti gli indirizzi di gruppo Data Secure. Assegna il suo indirizzo individuale come mittente in SharKNX. In questo modo l'accesso di SharKNX rimane nettamente separato dagli altri client.

2. **Collegare gli indirizzi di gruppo Data Secure all'interfaccia di tunneling del gateway.** In ETS, associa gli indirizzi di gruppo Data Secure all'interfaccia di connessione di tunneling del tuo gateway KNX IP Secure. Qualsiasi client che si connetterà attraverso quell'interfaccia (incluso SharKNX) verrà quindi riconosciuto come mittente attendibile dai dispositivi di campo.

> Se ti stai connettendo senza KNX IP Secure (tunnel standard non cifrato), SharKNX può utilizzare qualsiasi indirizzo individuale tu decida di configurare come mittente, e questo vincolo non viene applicato.

---

## Chiavi dello Strumento (Tool Keys) per la Gestione dei Dispositivi

KNX Data Secure si applica anche alle operazioni di gestione dei dispositivi (device management) - come la lettura delle info del dispositivo, l'attivazione della modalità di programmazione, il reset di un dispositivo, la programmazione di un indirizzo individuale o la lettura delle tabelle di comunicazione. I dispositivi che richiedono l'autenticazione a livello di strumento rifiuteranno i comandi di gestione provenienti da sorgenti sconosciute.

Quando carichi un file `.knxkeys` nella scheda **Security** della pagina Discovery, SharKNX estrae automaticamente tutte le **chiavi dello strumento (tool keys)** presenti nel file e le memorizza. Queste chiavi abilitano la comunicazione crittografata di gestione con i corrispondenti dispositivi Data Secure - non è richiesta alcuna configurazione aggiuntiva una volta caricate le chiavi.

Le chiavi dello strumento sono separate dalle chiavi di gruppo integrate nel file `.knxproj`. Se la tua installazione utilizza la gestione dei dispositivi Data Secure, avrai bisogno del file `.knxkeys` (o del file `.knxproj`, che contiene anch'esso le chiavi dello strumento) caricato nella scheda Security, oltre al progetto caricato nella pagina Project.

---

## Ulteriori Letture

Per una spiegazione tecnica dettagliata del protocollo KNX Data Secure, la nota applicativa di ABB "i-bus KNX Data Secure" è una risorsa approfondita che tratta in dettaglio i meccanismi crittografici, la gestione dei numeri di sequenza e la configurazione all'interno di ETS.

---

## KNX Data Secure vs. KNX IP Secure

| | KNX Data Secure | KNX IP Secure |
|---|---|---|
| **Ambito di applicazione** | Telegramma KNX (livello applicativo) | Livello di trasporto IP |
| **Cosa cifra** | Singoli telegrammi di gruppo sul mezzo KNX | Il tunnel UDP/TCP o il canale multicast |
| **Tipo di credenziale** | Chiave di gruppo per indirizzo di gruppo; chiavi dello strumento per dispositivo | Credenziali dell'interfaccia; chiave della dorsale (backbone) |
| **Dove si configura in SharKNX** | Pagina Project (chiavi da `.knxproj`); scheda Security (chiavi dello strumento) | Pagina Discovery → scheda Security |
| **Richiesto per** | Inviare/ricevere telegrammi di gruppo protetti | Connettersi a un gateway KNX IP Secure |

I due meccanismi sono indipendenti e possono essere utilizzati separatamente o congiuntamente. Consulta la sezione [KNX IP Secure](knx-ip-secure.md) per la controparte a livello di trasporto.
