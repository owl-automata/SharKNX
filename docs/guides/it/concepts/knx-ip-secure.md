# KNX IP Secure

KNX IP Secure è l'estensione di sicurezza a livello di trasporto del protocollo KNXnet/IP. Cifra la comunicazione tra un dispositivo KNX IP (gateway o router) e un client come SharKNX, impedendo l'intercettazione dei dati e il controllo non autorizzato attraverso la rete IP.

> Questa pagina spiega cos'è KNX IP Secure e come viene gestito da SharKNX. Per la procedura di configurazione dettagliata passo dopo passo, consulta la guida [Configurare KNX IP Secure](../how-to/setup-knx-ip-secure.md).

---

## Cosa Protegge KNX IP Secure

In un'installazione KNXnet/IP standard, il traffico di tunneling tra un client e un gateway viaggia sotto forma di pacchetti UDP non cifrati. Chiunque abbia accesso alla rete può catturare i telegrammi o iniettare comandi arbitrari. KNX IP Secure risolve questo problema spostando il trasporto del tunneling su protocollo **TCP** e applicando la cifratura AES-128 CCM alla sessione, garantendo che:

- Solo i client in possesso delle credenziali corrette possano stabilire una connessione.
- Il traffico non possa essere letto o reinviato (attacco replay) da altri nodi sulla rete.
- Il gateway possa rifiutare i tentativi di connessione provenienti da sorgenti sconosciute.

KNX IP Secure opera a livello di trasporto IP. Non modifica il contenuto del telegramma KNX in sé - questo è invece il compito di [KNX Data Secure](knx-data-secure.md).

---

## Le Due Modalità di KNX IP Secure

### Secure Tunneling (Tunneling Sicuro)

Il tunneling sicuro stabilisce una connessione **TCP** crittografata tra SharKNX e un'interfaccia compatibile con KNX IP Secure (tipicamente un gateway KNX IP o l'interfaccia di tunneling di un router KNX IP), sostituendo il trasporto UDP utilizzato dal tunneling KNXnet/IP standard. Ogni connessione di tunneling ha il proprio indirizzo individuale dell'interfaccia e un set corrispondente di credenziali nel portachiavi (keyring).

**Vincolo dell'indirizzo mittente:** Quando si è connessi tramite un tunnel KNX IP Secure, l'indirizzo individuale utilizzato nei telegrammi in uscita è fissato sul valore dell'interfaccia di tunneling assegnata dal gateway. SharKNX non può sovrascrivere questo valore. Questo aspetto è fondamentale quando si lavora con indirizzi di gruppo KNX Data Secure, i quali convalidano l'indirizzo individuale del mittente - vedi la sezione [KNX Data Secure](knx-data-secure.md) per i dettagli.

### Secure Multicast (IP Routing Secure)

I router KNX IP che supportano la funzionalità IP Routing Secure utilizzano una chiave simmetrica condivisa - la **chiave di dorsale (backbone key)** - per cifrare il traffico multicast sul gruppo multicast `224.0.23.12` tramite **UDP**. Tutti i nodi partecipanti sulla dorsale devono utilizzare la medesima chiave.

SharKNX supporta il multicast sicuro. Quando viene rilevato un router KNX IP, la scheda **Discover** mostra sia un'opzione multicast standard sia un'opzione multicast sicuro. La selezione dell'opzione multicast sicuro richiede il caricamento della chiave di dorsale.

---

## File delle Credenziali

Le credenziali KNX IP Secure vengono distribuite tramite ETS come parte del portachiavi (keyring) del progetto. SharKNX accetta le credenziali in tre formati:

| Formato | Cosa contiene | Note |
|---|---|---|
| `.knxkeys` | Credenziali dell'interfaccia, chiave di dorsale, chiavi dello strumento | Cifrato con una password specifica del progetto impostata in ETS |
| `.knxproj` | Progetto ETS completo incluso il portachiavi integrato | SharKNX estrae le credenziali automaticamente |
| Chiave di dorsale manuale | Singola chiave simmetrica, inserita come valore esadecimale (hex) | Solo per multicast sicuro; da utilizzare quando si dispone solo della chiave e non dell'intero file del portachiavi |

**Esportare il file `.knxkeys` da ETS:** Apri il tuo progetto in ETS. Dalla panoramica del progetto (all'esterno dell'editor di progetto), vai su **Altri dettagli → Sicurezza**, quindi seleziona **Backup del portachiavi**. Imposta una password e salva il file.

> **Convalida della password:** SharKNX non può verificare se la password di un file `.knxkeys` sia corretta al momento dell'importazione - questa è una caratteristica strutturale della specifica KNX. La password viene convalidata solo durante il tentativo effettivo di connessione. Se la connessione fallisce con un errore di autenticazione, verifica che la password corrisponda a quella impostata durante l'esportazione del portachiavi da ETS.

---

## Dove Caricare le Credenziali in SharKNX

Le credenziali possono essere caricate in tre punti diversi dell'app:

**Scheda Security (pagina Discovery):** È la scheda dedicata alla gestione di tutte le credenziali di sicurezza. Tocca il FAB a forma di scudo per aprire la schermata di importazione delle credenziali. Dopo il caricamento, la scheda mostra un riepilogo di ciò che è stato importato: quante interfacce sono state trovate e quanti dispositivi KNX Data Secure erano presenti nel file. Un pulsante cronologia consente di ricaricare rapidamente i file utilizzati di recente.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-ip-secure/knx-ip-secure-security-tab.png" width="320" alt="Scheda Security che mostra un file di credenziali caricato con il conteggio di interfacce e dispositivi" />
</div>

**Scheda del gateway (scheda Discovery):** Se un gateway rilevato segnala il supporto a KNX IP Secure, la sua scheda di dettaglio include il pulsante **Load Credentials** (Carica credenziali). Le credenziali caricate da qui vengono memorizzate nello stesso modo descritto per la scheda Security.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-ip-secure/knx-ip-secure-gateway-card.png" width="320" alt="Menu a comparsa inferiore con i dettagli del gateway contenente il pulsante Load Credentials per un gateway KNX IP Secure" />
</div>

**Menu di ottimizzazione della pagina Discovery:** L'icona delle impostazioni di ottimizzazione (tune icon) nella barra superiore della pagina Discovery fornisce un accesso rapido per caricare le credenziali da un file `.knxkeys` o `.knxproj` senza dover navigare fino alla scheda Security.

Le credenziali vengono memorizzate in modo persistente e rimangono disponibili anche dopo il riavvio dell'applicazione. Il caricamento di un nuovo file sostituisce le credenziali precedentemente memorizzate.

---

## Chiavi dello Strumento (Tool Keys) KNX Data Secure

Quando un file `.knxkeys` contiene le chiavi dello strumento per i dispositivi KNX Data Secure, SharKNX memorizza automaticamente anche tali chiavi. Ciò consente di eseguire operazioni crittografate di gestione dei dispositivi (device management) - come l'attivazione della modalità di programmazione, la lettura delle info del dispositivo, il reset di un dispositivo o la lettura delle tabelle di comunicazione - su dispositivi che richiedono l'autenticazione a livello di strumento. Queste chiavi sono separate dalle credenziali del tunnel IP Secure e vengono utilizzate per la comunicazione a livello di dispositivo su KNX TP.

---

## KNX IP Secure vs. KNX Data Secure

| | KNX IP Secure | KNX Data Secure |
|---|---|---|
| **Ambito di applicazione** | Livello di trasporto IP | Telegramma KNX (livello applicativo) |
| **Cosa cifra** | Il tunnel UDP/TCP o il canale multicast | Singoli telegrammi di gruppo sul mezzo KNX |
| **Tipo di credenziale** | Credenziali dell'interfaccia, chiave di dorsale | Chiave di gruppo per indirizzo di gruppo |
| **Dove si configura** | Pagina Discovery → scheda Security | Pagina Project (caricata con il file `.knxproj`) |
| **Richiesto per** | Connettersi a un gateway sicuro | Inviare/ricevere telegrammi di gruppo protetti |

I due meccanismi sono indipendenti. Un'installazione può utilizzare KNX IP Secure per la connessione IP senza utilizzare KNX Data Secure sul bus, o viceversa, oppure entrambi contemporaneamente.

Consulta la sezione [KNX Data Secure](knx-data-secure.md) per scoprire come SharKNX gestisce la cifratura a livello di singolo telegramma.
