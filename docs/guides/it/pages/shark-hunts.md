# Pagina Shark Hunts (Sessioni di Test/Collaudo)

La pagina Shark Hunts è la sezione in cui è possibile creare, gestire ed eseguire le **shark hunts** - set riutilizzabili di azioni di invio KNX e filtri di monitoraggio salvati come file JSON portatili. Una "hunt" fornisce una pagina dedicata con azioni attivabili con un singolo tocco, filtri preconfigurati e un gateway integrato opzionale, pronta per essere condivisa con colleghi o clienti.

Per comprendere il concetto alla base di questa funzione, vedi [Shark Hunts](../concepts/shark-hunts.md).

---

## Layout della Pagina Principale

Al di sotto della barra superiore è presente una riga per il filtro testuale. Digita del testo per filtrare le schede delle hunt in base al nome. L'**icona della stella** sulla destra della riga applica immediatamente un filtro per mostrare solo le hunt contrassegnate come preferite.

La barra superiore contiene:

- **Pulsante Help (Aiuto)** - apre una pagina di riferimento interna all'app che illustra il concetto di Shark Hunt, i tipi di azione ed esempi pratici.
- **Icona delle regolazioni (Tune icon)** - offre due azioni:
  - **Export Hunts** - esporta tutte le hunt esistenti in un unico file JSON.
  - **Import Hunts** - importa un file JSON contenente una o più hunt.

### Creare una Hunt

Tocca il **FAB "+"** per aprire la procedura guidata (wizard) di creazione in cinque passaggi. Vedi [Creare una Shark Hunt](../how-to/create-shark-hunt.md) per una guida passo-passo completa.

### Schede delle Hunt (Hunt Cards)

Ogni hunt creata appare sotto forma di scheda. Il colore del bordo superiore della scheda indica la sua tipologia:

| Colore del bordo | Tipo di Hunt |
|---|---|
| Verde | Solo azioni di invio (Send) |
| Blu | Solo azioni di monitoraggio (Monitor) |
| Rosso | Sia azioni di invio che di monitoraggio |

Ogni scheda mostra il nome della hunt, la descrizione (se presente) e l'etichetta del tipo. Presenta inoltre:

- **Icona della stella** - consente di contrassegnare o rimuovere la hunt dai preferiti.
- **Menu a tre punti** - Modifica (Edit), Esporta (singolo JSON), Condividi, Elimina e Info.
  - **Info** apre una schermata con nome, tipo, stato dei preferiti, conteggio e nomi delle azioni, e i timestamp di creazione/modifica.

Tenendo premuto a lungo su una scheda qualsiasi si entra nella modalità di selezione multipla, che consente di copiare, esportare o eliminare più hunt contemporaneamente.

Le schede delle hunt sono persistenti e rimangono memorizzate al riavvio dell'applicazione.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/shark-hunts/shark-hunts-main.png" width="320" alt="Pagina principale delle Shark Hunts che mostra le schede delle hunt con bordi superiori codificati per colore e riga dei filtri" />
</div>

---

## Pagina di Dettaglio della Hunt

Toccando la scheda di una hunt si apre la sua pagina dedicata. La barra superiore mostra un pulsante indietro e un campo di filtro per cercare all'interno delle schede delle azioni in questa pagina.

### Riga dei Badge

| Badge | Descrizione |
|---|---|
| **Nome della hunt** | Toccandolo si apre la schermata informativa della hunt (nome, tipo, preferito, conteggio azioni, timestamp). |
| **Stato connessione** | Rosso = disconnesso, Verde = connesso. Toccandolo avvia o interrompe la connessione con il gateway. |
| **ETS Project** | Mostra se è caricato un progetto ETS. Toccandolo si apre una schermata con i dettagli del progetto (nome, formato GA, date) e un pulsante per caricare o rimuovere il progetto. |
| **Data Secure** | Mostra lo stato del mittente KNX Data Secure. Grigio = nessuna GA Data Secure caricata; ambra = GA presenti ma nessun mittente configurato (tocca per configurare); verde = mittenti configurati (tocca per verificare). |
| **Gateway** | Mostra l'indirizzo IP del gateway selezionato. Blu = selezionato, grigio = nessuno selezionato, verde = selezionato e connesso. Toccandolo si apre una schermata con i dettagli del gateway e un pulsante per cancellare la selezione (quando non è attivo il monitor). |

### Connessione

Tocca il **FAB verde Connect** per connetterti al gateway configurato. Se non è stato selezionato alcun gateway, una finestra a comparsa elencherà le opzioni disponibili - inclusi gli eventuali gateway integrati nella hunt durante la creazione, oltre agli altri gateway rilevati e configurati manualmente. Una volta connesso, il FAB diventa rosso con un'icona di stop per consentire la disconnessione.

Tutte le schede delle azioni rimangono in trasparenza e non sono interattive finché il dispositivo non è connesso.

---

## Sezione Azioni di Invio (Send Actions)

Le schede delle azioni di invio sono raggruppate nella sezione superiore della pagina della hunt. Toccando una scheda, l'azione viene eseguita immediatamente:

- **Azione fissa (Fixed action)** - invia il valore preconfigurato senza richiedere alcuna conferma.
- **Azione multipla / Sequenza** - invia tutti i comandi in sequenza, rispettando gli eventuali ritardi (delay) configurati tra l'uno e l'altro.
- **Azione variabile** - apre una schermata inferiore con un'interfaccia di input appropriata al tipo di datapoint (DPT) (es. cursori colore per RGB, un cursore percentuale per il DPT 5.001). Conferma l'invio con il pulsante apposito.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/shark-hunts/shark-hunts-hunt-page.png" width="320" alt="Pagina di dettaglio della hunt che mostra le schede delle azioni di invio nella sezione superiore e le schede delle azioni di monitoraggio in basso" />
</div>

---

## Sezione Azioni di Monitoraggio (Monitor Actions)

Le schede delle azioni di monitoraggio sono raggruppate al di sotto delle azioni di invio. Toccando una scheda si apre lo **Shark Hunt Monitor** per quella specifica azione - ovvero una sessione di monitoraggio con i filtri dell'azione applicati istantaneamente.

### Shark Hunt Monitor

La pagina Shark Hunt Monitor è simile alla [pagina Monitor](monitor.md) principale, ma è circoscritta al filtro dell'azione attiva. La barra superiore mostra il nome della hunt come titolo e il nome dell'azione di monitoraggio come sottotitolo, oltre a un pulsante di **salvataggio/esportazione** (attivo quando sono presenti telegrammi).

#### Riga dei Badge

| Badge | Descrizione |
|---|---|
| **Send** | Apre una schermata inferiore per comporre e inviare un comando. Mostra anche i pulsanti rapidi (chip) per i comandi recenti; tieni premuto a lungo su un chip per riaprire il compositore con i campi precompilati. |
| **Dettagli filtro** | Mostra le condizioni del filtro attualmente attivo. |
| **Clear** | Svuota tutti i telegrammi dall'elenco. |
| **Data Secure** | Identico al badge Data Secure della pagina di dettaglio della hunt. |
| **View** | Ordinamento (dal più recente / dal più vecchio) e formato dell'indirizzo di gruppo. Influisce sui nuovi telegrammi in ingresso. |
| **Statistics** | Telegrammi totali, frequenza telegrammi/sec, indirizzi di gruppo più attivi, dispositivi sorgente più attivi e tipologie di telegrammi principali. |
| **Gateway** | Identico al badge gateway della pagina di dettaglio della hunt. |

I **FAB del monitor** funzionano come segue:
- FAB grande - verde/start per avviare il monitoraggio, rosso/stop per terminarlo.
- FAB piccolo sovrastante - apre una schermata con l'elenco di tutte le azioni di monitoraggio presenti in questa hunt, consentendo di cambiare filtri senza abbandonare la pagina. L'azione attualmente attiva è contrassegnata da un pallino verde.

#### Elenco dei Telegrammi

Ogni riga di telegramma mostra:
- Indirizzo individuale mittente → indirizzo di gruppo di destinazione
- Nome dell'indirizzo di gruppo | valore | valore esadecimale grezzo (nome e valore richiedono un progetto ETS caricato)
- Timestamp nel formato ORE:MINUTI:SECONDI.ms

Toccando una riga si apre la schermata dei dettagli del telegramma con tutti i campi completi (tempo, sorgente, destinazione, nome, valore, payload grezzo) e due pulsanti di azione - **Read** (invia un comando di lettura all'indirizzo di gruppo) e **Write** (apre il compositore di comandi precompilato con indirizzo e DPT). Un terzo pulsante, **Plot**, apre una vista grafico a due schede: un grafico a serie temporale del valore dell'indirizzo di gruppo e un grafico a barre degli indirizzi individuali sorgente.

#### Esportazione

La schermata di esportazione consente di assegnare un nome al file (precompilato con un timestamp), scegliere quali colonne includere (ID, tempo, sorgente, destinazione, nome, tipo, valore, dato grezzo), impostare il numero di telegrammi da esportare, attivare o disattivare le intestazioni delle colonne e scegliere un delimitatore (virgola, tabulazione o punto e virgola).
