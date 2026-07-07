# Pagina Project (Progetto)

La pagina Project è la seconda schermata presente nella barra di navigazione inferiore. In questa sezione è possibile caricare un file di progetto ETS e sfogliarne i contenuti attraverso quattro viste strutturate: Group Addresses, Devices, Topology e Buildings.

---

## Caricamento di un Progetto

Tocca il **FAB della cartella** (pulsante d'azione fluttuante) per aprire il selettore di file e selezionare un file `.knxproj`. Se hai già caricato dei progetti in passato, apparirà prima una schermata con la cronologia - seleziona una voce recente o tocca **Browse (Sfoglia)** per scegliere un nuovo file. L'applicazione supporta i progetti protetti da password; in tal caso, richiederà l'inserimento della password durante la fase di importazione.

Il caricamento di un nuovo progetto sostituisce integralmente quello attualmente attivo. I dati del progetto precedente verranno svuotati dalla memoria.

> Per maggiori dettagli su cosa comporta l'importazione di un progetto, vedi [I progetti ETS in SharKNX](../concepts/ets-project-in-sharknx.md).

---

## Barra di Ricerca e Filtro

Una volta caricato un progetto, al di sotto della barra delle schede apparirà una barra di ricerca e filtro. Digita qualsiasi testo per effettuare una ricerca globale su tutti i nomi presenti nel progetto - indirizzi di gruppo, dispositivi, edifici, linee e funzioni. I risultati si aggiornano istantaneamente durante la digitazione all'interno della scheda attiva.

Accanto alla barra di ricerca è presente il pulsante **Expand All / Collapse All (Espandi tutto / Comprimi tutto)** che consente di espandere o comprimere contemporaneamente tutte le sezioni ad albero della scheda corrente.

---

## Banner KNX Data Secure

Se il progetto caricato contiene indirizzi di gruppo KNX Data Secure, sotto la barra delle schede apparirà un banner che invita a configurare i mittenti Data Secure (Data Secure Senders). Toccando il banner verrai indirizzato alla pagina di configurazione dei mittenti, dove potrai impostare quale indirizzo individuale SharKNX debba utilizzare come mittente per ciascun indirizzo di gruppo sicuro. Questa configurazione è obbligatoria per l'invio di comandi Data Secure; il monitoraggio, invece, funziona anche senza questo passaggio. Per maggiori dettagli, vedi [KNX Data Secure](../concepts/knx-data-secure.md).

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-data-secure-banner.png" width="320" alt="Pagina Project con il banner data secure sotto la barra delle schede dopo il caricamento di un progetto con indirizzi di gruppo sicuri" />
</div>

---

## Scheda Group Addresses (Indirizzi di Gruppo)

Questa scheda mostra la gerarchia degli indirizzi di gruppo esattamente come configurata in ETS: i gruppi principali (main groups) al primo livello, espandibili nei gruppi intermedi (middle groups) e, infine, nei singoli indirizzi di gruppo.

Tocca qualsiasi gruppo principale o intermedio per espanderlo o comprimerlo. Tocca un singolo **indirizzo di gruppo** per aprire la schermata delle azioni rapide, che mostra:
- Nome dell'indirizzo di gruppo
- Tipo e sottotipo di datapoint (DPT)
- Pulsante **Read (Lettura)** - invia una richiesta di lettura sul bus e mostra la risposta direttamente all'interno della schermata entro 1 secondo (se perviene una risposta)
- Pulsante **Write (Scrittura)** - apre il compositore di comandi con l'indirizzo di gruppo e il DPT precompilati; inserisci il valore e invia

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-group-addresses.png" width="320" alt="Scheda Group Addresses che mostra l'albero del gruppo principale espanso fino ai singoli indirizzi di gruppo" />
</div>

> È necessario selezionare un gateway per poter inviare comandi di lettura o scrittura. Se non ne è configurato alcuno, l'applicazione richiederà di sceglierne uno.

---

## Scheda Devices (Dispositivi)

Questa scheda elenca tutti i dispositivi presenti nel progetto, ordinati per indirizzo individuale. I dispositivi che hanno indirizzi di gruppo collegati possono essere espansi per mostrare tali indirizzi - tocca uno di essi per aprire la medesima schermata di azione rapida descritta nella scheda Group Addresses.

Effettua un **tocco singolo** su un dispositivo senza indirizzi di gruppo, oppure una **pressione prolungata** su un dispositivo con indirizzi di gruppo, per aprire la **schermata dei dettagli del dispositivo**. Questa schermata contiene:

### Scheda Info Dispositivo
Una scheda compatta che indica se l'indirizzo individuale del dispositivo e il programma applicativo risultano caricati nel progetto ETS.

### Azioni Diagnostiche Rapide

| Azione | Descrizione |
|---|---|
| **Check** | Verifica se il dispositivo è presente e risponde sul bus |
| **Read Info** | Legge le informazioni dettagliate direttamente dal dispositivo (vedi sotto) |
| **Toggle Programming Mode** | Attiva o disattiva da remoto la modalità di programmazione del dispositivo |
| **Program Address** | Scansiona i dispositivi in modalità di programmazione e scrive un nuovo indirizzo individuale |

L'azione **Read Info** recupera i seguenti dati dal dispositivo:
- Descrittore del dispositivo (es. System B)
- Stato della modalità di programmazione
- Produttore e codice d'ordine
- Versione del firmware
- Stato di caricamento (load state) e stato di esecuzione (run state)
- Versione dell'applicazione
- Stato della tabella degli indirizzi e della tabella delle associazioni
- Lunghezza massima APDU
- Tipo di hardware
- Flag di errore e stato del dispositivo

### Pulsante Communication Objects (Oggetti di Comunicazione)

Apre la pagina dedicata agli **Oggetti di Comunicazione** di questo specifico dispositivo (vedi sotto).

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-device-detail.png" width="320" alt="Schermata inferiore dei dettagli del dispositivo che mostra la scheda informativa, i quattro pulsanti di azione rapida e il pulsante Communication Objects" />
</div>

---

## Pagina Communication Objects

Accessibile dal pulsante Communication Objects nella schermata dei dettagli del dispositivo. Questa pagina mostra tutti gli oggetti di comunicazione del dispositivo che risultano collegati ad almeno un indirizzo di gruppo.

Nella parte superiore, la pagina mostra la data di **ultima modifica** e di **ultimo download da ETS** del dispositivo.

Ogni voce relativa a un oggetto di comunicazione mostra:
- Numero dell'oggetto
- Flag: Lettura (R), Scrittura (W), Comunicazione (C), Trasmissione (T), Aggiornamento (U), Lettura all'inizializzazione (I)
- Nome della funzione (se disponibile nell'applicazione del dispositivo)
- Dimensione dell'oggetto (es. 1 bit, 1 byte, 2 byte)
- Indirizzi di gruppo collegati - ciascuno è interattivo e permette di aprire la schermata di azione rapida per i comandi di lettura/scrittura

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-comm-objects.png" width="320" alt="Pagina Communication Objects che mostra un elenco di oggetti di comunicazione con flag, dimensione e indirizzi di gruppo collegati" />
</div>

> L'opzione **Load communication objects** nelle Impostazioni Progetto controlla se questi dati debbano essere analizzati (parsed) al momento del caricamento. È abilitata per impostazione predefinita. Disabilitarla riduce l'utilizzo della memoria per i progetti molto grandi, ma impedisce l'accesso a questa pagina.

---

## Scheda Topology (Topologia)

Questa scheda mostra la topologia fisica del progetto: le aree al livello principale, espandibili in linee o segmenti e, infine, nei singoli dispositivi. Tocca qualsiasi dispositivo per aprire la medesima schermata dei dettagli del dispositivo descritta in precedenza.

---

## Scheda Buildings (Edifici)

Questa scheda mostra la struttura degli edifici così come configurata in ETS: edifici e piani espandibili in locali (stanze) e funzioni, con i relativi indirizzi di gruppo e dispositivi associati. Tocca qualsiasi indirizzo di gruppo o dispositivo per aprire le rispettive schermate di azione rapida.

---

## Menu di Ottimizzazione (Tune Menu)

L'icona delle regolazioni nella barra superiore apre una schermata inferiore con un'unica azione disponibile:

**Unload project (Rimuovi progetto)** - rimuove dalla memoria il progetto attualmente caricato. Tutte e quattro le schede torneranno allo stato vuoto iniziale. I telegrammi già acquisiti nella pagina Monitor rimarranno visibili, ma perderanno i loro nomi descrittivi e i valori decodificati associati al progetto.
