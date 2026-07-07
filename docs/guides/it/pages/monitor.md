# Pagina Monitor (Monitoraggio Bus)

La pagina Monitor fornisce una sessione di monitoraggio in tempo reale del bus KNX. I telegrammi in ingresso vengono catturati istantaneamente e visualizzati all'interno di un elenco scorrevole. È possibile filtrare, ispezionare, tracciare ed esportare i telegrammi, oltre a inviare comandi sul bus senza mai abbandonare la pagina.

---

## Avvio e Arresto

Tocca il **FAB verde di avvio** (pulsante fluttuante) per iniziare una sessione di monitoraggio.

- Se non è stato selezionato alcun gateway, apparirà un selettore contenente i gateway rilevati e salvati. Selezionane uno per procedere.
- L'applicazione si connette al gateway e inizia immediatamente a catturare i telegrammi.
- Mentre il monitor è attivo, il FAB fluttuante diventa un **FAB rosso di invio** (vedi [Invio di Comandi](#invio-di-comandi)).

Tocca il **badge Start/Stop** nella riga dei badge (vedi sotto) per arrestare il monitor. L'elenco dei telegrammi rimane visibile anche dopo l'arresto - non verrà svuotato finché non deciderai esplicitamente di cancellarlo.

---

## Riga dei Filtri (Filter Bar Row)

La riga della barra dei filtri è bloccata sopra l'elenco dei telegrammi e rimane sempre visibile.

**Barra di filtro testuale** - digita del testo per filtrare l'elenco dei telegrammi visibili. La ricerca viene effettuata sul nome degli indirizzi di gruppo, sui valori e sugli indirizzi individuali. L'elenco sottostante non viene modificato; cancella il filtro per visualizzare nuovamente tutti i telegrammi catturati.

**Icona di ricerca con filtro** - apre una schermata inferiore suddivisa in due schede: una elenca tutti gli indirizzi di gruppo del tuo progetto ETS caricato, l'altra tutti i dispositivi. Tocca una voce qualsiasi per applicarla immediatamente come filtro attivo. Molto utile per isolare rapidamente uno specifico indirizzo di gruppo o un dispositivo senza dover digitare.

**Pulsante Always-on-top (Sempre in primo piano)** - quando abilitato (impostazione predefinita), l'elenco scorre automaticamente verso l'ultimo telegramma ricevuto. La schermata rileva in automatico quando stai scorrendo l'elenco manualmente e mette in pausa lo scorrimento automatico fino a quando non ritorni in cima. Toccando il pulsante quando è disabilitato, la vista salta immediatamente all'inizio dell'elenco.

**Pulsante Export (Esporta)** - apre la schermata inferiore per l'esportazione. Vedi [Esportazione dei Telegrammi](#esportazione-dei-telegrammi).

---

## Riga dei Badge

Una riga scorrevole di badge è bloccata al di sotto della barra dei filtri. Ogni badge è interattivo.

### Start / Stop
Avvia o arresta la sessione del monitor. Svolge la medesima funzione del FAB verde prima che il monitor sia attivo.

### Clear (Cancella)
Svuota l'elenco da tutti i telegrammi. Se attiva, la sessione di monitoraggio continua a rimanere in esecuzione.

### ETS Project
Mostra se è presente un progetto ETS caricato. Toccandolo si apre una schermata con i dettagli del progetto (nome, formato degli indirizzi di gruppo, date di creazione e modifica) e un pulsante per rimuovere il progetto. Se non è caricato alcun progetto, la schermata presenterà il pulsante **Load Project**, che apre lo stesso selettore di file della pagina Project.

### Data Secure
Riflette lo stato di KNX Data Secure per la sessione corrente:

| Stato del badge | Significato |
|---|---|
| Grigio | Nessun indirizzo di gruppo Data Secure presente nel progetto ETS caricato |
| Ambra | Indirizzi Data Secure presenti, ma i mittenti (senders) non sono configurati |
| Verde | Indirizzi Data Secure presenti e mittenti configurati correttamente |

Toccando un badge di colore ambra si apre una schermata con un pulsante per navigare direttamente alla pagina di configurazione dei mittenti Data Secure (Data Secure Senders). Vedi [KNX Data Secure](../concepts/knx-data-secure.md).

### Telegrams (Telegrammi)
Mostra il conteggio attuale dei telegrammi ricevuti. Toccandolo si apre una schermata contenente:
- **Clear filter** - rimuove qualsiasi filtro testuale o di ricerca attivo (visibile solo quando un filtro è attivo)
- **Clear telegrams** - svuota tutti i telegrammi catturati
- **Statistics** - apre una vista statistica avanzata che mostra:
  - Conteggio totale dei telegrammi
  - Frequenza telegrammi/secondo (calcolata dal timestamp del primo all'ultimo telegramma)
  - Indirizzi di gruppo più attivi (espressi in percentuale sul totale)
  - Indirizzi individuali dei mittenti più attivi (espressi in percentuale)
  - Tipologie di telegrammi più frequenti (scrittura, lettura, risposta, ecc. in percentuale)

### View (Visualizzazione)
Apre le opzioni di visualizzazione dedicate all'elenco dei telegrammi:
- **Ordinamento** - dal più recente (predefinito) o dal più vecchio
- **Formato degli indirizzi** - modalità di visualizzazione degli indirizzi di gruppo (a 3 livelli, a 2 livelli o libero). Impostato sul formato del progetto ETS caricato. Le modifiche influiscono solo sui nuovi telegrammi in ingresso e non su quelli già visibili.
- **View Group** - naviga verso una seconda schermata in cui è possibile filtrare l'elenco visibile per indirizzo di gruppo, indirizzo fisico, tipo di telegramma o priorità. Selezionando una voce verranno mostrati solo i telegrammi corrispondenti.

### Gateway
Mostra l'indirizzo IP del gateway attualmente selezionato. Il colore indica lo stato della connessione:

| Colore | Stato |
|---|---|
| Grigio | Nessun gateway selezionato |
| Blu | Gateway selezionato, non connesso |
| Verde | Selezionato e connesso |

Toccandolo si apre una schermata con i dettagli del gateway e il pulsante **Clear selection** (disponibile solo quando il monitor è fermo).

---

## Elenco dei Telegrammi

Ogni riga all'interno dell'elenco mostra:
- **Indirizzo individuale mittente → indirizzo di gruppo di destinazione**
- **Nome dell'indirizzo di gruppo** *(richiede progetto ETS)* | **valore decodificato** *(richiede progetto ETS)* | **payload esadecimale grezzo (raw hex)**
- **Timestamp** nel formato `ORE:MINUTI:SECONDI.ms`

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-active.png" width="320" alt="Pagina monitor con telegrammi in tempo reale nella vista elenco" />
</div>

### Schermata dei Dettagli del Telegramma

Tocca una riga qualsiasi per aprire la schermata dei dettagli di quel singolo telegramma. Mostra:

- Timestamp
- Indirizzo individuale sorgente
- Indirizzo di gruppo di destinazione
- Nome dell'indirizzo di gruppo *(se il progetto ETS è caricato)*
- Valore decodificato *(se il progetto ETS è caricato)*
- Payload esadecimale grezzo (raw hex)

Sono disponibili due pulsanti di azione immediata:
- **Read (Lettura)** - invia immediatamente un comando di lettura all'indirizzo di gruppo del telegramma
- **Write (Scrittura)** - apre il compositore di comandi con l'indirizzo di gruppo e il tipo di datapoint (DPT) già precompilati; inserisci il valore e invia

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-telegram-detail.png" width="320" alt="Schermata dei dettagli del telegramma con tempo, sorgente, destinazione, valore e pulsanti Read, Write e Plot" />
</div>

### Grafici (Plot)

Il pulsante **Plot** all'interno della schermata dei dettagli apre una vista grafico a due schede per l'indirizzo di gruppo selezionato:

- **Scheda Value** - un grafico a serie temporale di tutti i valori catturati per questo specifico indirizzo. Puoi fare "pinch-to-zoom" per ingrandire, scorrere orizzontalmente e toccare un punto per leggerne il valore esatto e il timestamp.
- **Scheda Sources** - un grafico a barre degli indirizzi individuali dei mittenti che hanno trasmesso su questo indirizzo di gruppo, estremamente utile per identificare mittenti imprevisti o diagnosticare anomalie ("rumore") sul bus.

Una scheda informativa riepiloga l'intervallo di tempo coperto dai dati del grafico.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-plot.png" width="320" alt="Vista grafico che mostra una serie temporale del valore di un indirizzo di gruppo nel tempo" />
</div>

---

## Invio di Comandi

Mentre il monitor è in esecuzione, il FAB fluttuante diventa un **FAB rosso di invio**. Toccandolo si apre una schermata inferiore che contiene:

- **New Command** - apre il compositore di comandi. Inserisci un indirizzo di gruppo (o cercalo nel progetto ETS caricato), seleziona l'operazione di scrittura o lettura, scegli il tipo e il sottotipo di datapoint (DPT), inserisci il valore e tocca **Send**. Il comando inviato apparirà immediatamente nell'elenco dei telegrammi.
- **Quick command chips (Invia comandi rapidi)** - al di sotto del pulsante per i nuovi comandi appaiono dei pulsanti rapidi (chip) relativi ai comandi inviati di recente. Tocca un chip per reinviare istantaneamente lo stesso identico comando. Tieni premuto a lungo su un chip per riaprire il compositore con i campi di quel comando già precompilati, consentendoti di regolare il valore prima dell'invio.

---

## Esportazione dei Telegrammi

La schermata inferiore di esportazione (accessibile dal pulsante di esportazione nella riga dei filtri o dal menu di ottimizzazione in alto) consente di salvare o condividere l'elenco attuale dei telegrammi sotto forma di file CSV.

Opzioni disponibili:

| Opzione | Descrizione |
|---|---|
| Nome file | Modificabile, precompilato automaticamente con un timestamp |
| Colonne | Caselle di selezione per includere id, tempo, sorgente, destinazione, nome, tipo, valore, dato grezzo (raw) |
| Conteggio telegrammi | Scegli quanti telegrammi esportare (es. gli ultimi 100 di 5000) |
| Includi intestazioni | Attiva o disattiva la riga di intestazione delle colonne nel file CSV |
| Delimitatore | Virgola (predefinito), tabulazione o punto e virgola |

Scegliendo **Save**, il file verrà scritto nella memoria del tuo dispositivo. Scegliendo **Share**, si aprirà la schermata di condivisione di sistema per inviare direttamente il file a un'app di messaggistica, a un servizio di cloud storage o via email.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/monitor/monitor-export.png" width="320" alt="Schermata inferiore di esportazione con campo di inserimento nome file, caselle di selezione colonne e pulsanti Save e Share" />
</div>

Vedi [Formati di Esportazione](../reference/export-format.md) per consultare la struttura completa del file CSV.

---

## Menu di Ottimizzazione (Tune Menu)

L'icona delle regolazioni nella barra superiore apre ulteriori azioni dedicate alla pagina Monitor:

**Import SharKNX CSV** - carica all'interno dell'elenco un file CSV precedentemente esportato da SharKNX. I telegrammi importati sostituiscono l'elenco corrente. Il file deve rispettare il formato di esportazione di SharKNX.

**Export telegrams** - esegue la medesima azione del pulsante di esportazione presente nella riga dei filtri.

**Import from ETS XML** - carica un file di esportazione dei telegrammi generato dal software ETS. Utile per visualizzare e analizzare sul tuo dispositivo mobile una registrazione effettuata in ETS, oppure per condividerla con i colleghi. Sostituisce l'elenco dei telegrammi corrente.

**Apply project data (Applica dati del progetto)** - dopo aver caricato o aggiornato un progetto ETS, questa funzione applica retroattivamente i nomi degli indirizzi di gruppo e i tipi di datapoint del progetto a tutti i telegrammi attualmente presenti nell'elenco. Il monitor deve essere arrestato prima di poter eseguire questa azione. Utilizzala quando carichi un progetto dopo aver già catturato dei telegrammi, o quando ricarichi un progetto aggiornato e desideri che i nuovi nomi si riflettano sui dati esistenti già acquisiti.
