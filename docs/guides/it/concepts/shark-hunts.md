# Shark Hunts

Una "Shark Hunt" è un set di azioni riutilizzabile e indipendente progettato per il test e la diagnostica di un'installazione KNX. Invece di dover navigare ogni volta verso un indirizzo di gruppo, selezionare un tipo di datapoint e comporre un comando, puoi creare una "Hunt" (Caccia) una sola volta ed eseguirla con un singolo tocco - da qualsiasi punto dell'applicazione e durante qualsiasi visita successiva al medesimo impianto.

---

## L'Idea di Base

Ogni Shark Hunt viene memorizzata sotto forma di file JSON che descrive una raccolta di **azioni di invio** (comandi inviati sul bus) e **azioni di monitoraggio** (sessioni del monitor con filtri applicati). Una Hunt può contenere l'una o l'altra tipologia di azione, oppure entrambe. Quando apri una Hunt, tutte le sue azioni vengono presentate all'interno di un'unica pagina sotto forma di schede interattive, pronte per essere avviate.

Questo rende le Shark Hunts estremamente utili in diversi scenari:

- **Test ripetitivi.** La messa in servizio (commissioning) richiede spesso l'invio dei medesimi comandi dozzine di volte nel corso di più visite in cantiere. Una Hunt memorizza tali comandi in modo da non doverli mai più ricostruire da zero.
- **Delega della diagnostica.** Una Hunt può includere tutti i dettagli di connessione relativi a una specifica installazione. Puoi esportarla e condividerla con un collega o con un cliente, il quale potrà eseguirla sul proprio dispositivo senza dover necessariamente sapere come configurare un gateway o come trovare un indirizzo di gruppo.
- **Sequenze di test strutturate.** Un'azione multipla o sequenziale consente di inviare una serie di comandi con ritardi (delay) configurabili tra l'uno e l'altro, permettendo di testare uno scenario di illuminazione completo o un ciclo di movimentazione delle tapparelle con un solo tocco.
- **Filtraggio avanzato del bus.** Le azioni di monitoraggio consentono di applicare logiche di filtraggio complesse - combinando intervalli di indirizzi di gruppo, filtri per dispositivo, filtri per tipo di telegramma e finestre temporali - che la barra di filtraggio standard del monitor non è in grado di gestire.

---

## Azioni di Invio (Send Actions)

Sono disponibili tre tipologie di azioni di invio:

**Send Fixed (Invio Fisso)** esegue ogni volta un singolo comando di scrittura o lettura verso uno specifico indirizzo di gruppo con un valore fisso. Risulta utile per l'attivazione rapida dei dispositivi - come accendere una luce, salvare uno scenario o verificare il valore di un sensore.

**Send Multiple / Sequence (Invio Multiplo / Sequenza)** esegue una serie di comandi fissi in ordine cronologico. Ogni comando all'interno della sequenza può avere un ritardo configurabile prima dell'attivazione del comando successivo (fino a un massimo di 10 secondi per singolo step). Utilizza questa opzione per testare il salvataggio di scenari, sequenze di movimentazione di tapparelle o qualsiasi logica di automazione multi-step.

**Send Variable (Invio Variabile)** invia un valore a tua scelta al momento dell'esecuzione a uno o più indirizzi di gruppo che condividono il medesimo tipo di datapoint (DPT). Quando tocchi la scheda dell'azione, si apre una schermata inferiore di inserimento del valore dotata dei controlli appropriati per quel DPT (slider, selettori di colore, campi numerici, ecc.). Utile quando desideri la flessibilità di testare valori differenti senza dover modificare la Hunt.

---

## Azioni di Monitoraggio (Monitor Actions)

Sono disponibili tre tipologie di azioni di monitoraggio:

**Custom Monitor (Monitor Personalizzato)** applica un filtro multi-condizione al monitor di bus. Le condizioni possono filtrare per indirizzo di gruppo (incluse le wildcard come `1/*/0`), per indirizzo individuale del mittente (incluse le wildcard come `1.*.*`), per tipo di telegramma (lettura, scrittura, risposta), per nome o testo descrittivo e per finestra temporale. Le condizioni sono collegate tramite logica AND/OR, abilitando filtri che non sarebbero esprimibili attraverso la barra di ricerca standard del monitor. Le voci relative a indirizzi e dispositivi possono anche essere impostate per escludere anziché includere, permettendoti così di monitorare tutto ad eccezione di uno specifico intervallo.

**Monitor Space (Monitor dell'Ambiente)** utilizza la struttura degli edifici del tuo progetto ETS per definire l'obiettivo del filtro. Selezionando una stanza o un ambiente dalla gerarchia dell'edificio, il monitor mostrerà esclusivamente gli indirizzi di gruppo o i dispositivi appartenenti a quello specifico spazio. Non è richiesto alcun inserimento manuale degli indirizzi.

**Monitor Device (Monitor del Dispositivo)** prende come target uno o più dispositivi specifici dal tuo progetto ETS e monitora tutti gli indirizzi di gruppo ad essi collegati. Ideale per isolare la comunicazione di un singolo attuatore o sensore durante le fasi di test.

Quando apri un'azione di monitoraggio all'interno di una Hunt, i filtri vengono applicati immediatamente. Un badge nella vista monitor mostra i dettagli del filtro attivo e un menu di selezione rapida ti consente di passare da un'azione di monitoraggio all'altra all'interno della Hunt senza mai dover uscire dalla pagina del monitor.

---

## Condivisione e Portabilità

Le Shark Hunts sono progettate per essere facilmente condivise. Ogni Hunt può opzionalmente includere un **gateway preconfigurato** - l'indirizzo IP, la porta e le impostazioni di connessione relative all'installazione per cui è stata creata. Quando un utente apre una Hunt condivisa, quel determinato gateway appare come opzione di connessione disponibile, consentendogli di connettersi ed eseguire la Hunt senza dover rilevare o configurare alcunché in autonomia.

Puoi esportare una singola Hunt o tutte le tue Hunt contemporaneamente sotto forma di file JSON, per poi condividerlo tramite qualsiasi metodo di trasferimento file - applicazioni di messaggistica, e-mail o servizi cloud. L'importazione di un file JSON aggiunge le Hunt in esso contenute alla tua lista personale senza sovrascrivere quelle già esistenti.

Le schede delle Hunt sono codificate per colore in modo da poterne identificare a colpo d'occhio la funzione:

| Colore del bordo | Contenuto |
|---|---|
| Verde | Solo azioni di invio |
| Blu | Solo azioni di monitoraggio |
| Rosso | Sia azioni di invio che di monitoraggio |

---

## Persistenza

Le Hunt vengono salvate in locale sul dispositivo e persistono anche dopo il riavvio dell'applicazione. I timestamp relativi alla creazione e all'ultima modifica di ciascuna Hunt vengono memorizzati e risultano visibili all'interno della schermata informativa della Hunt stessa.

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/concepts/shark-hunts/shark-hunts-main-page.png" width="320" alt="Pagina principale di Shark Hunts che mostra le schede delle Hunt con bordi codificati per colore" /></td>
      <td><img src="../../../../assets/screenshots/guides/concepts/shark-hunts/shark-hunts-hunt-page.png" width="320" alt="Una pagina aperta di Shark Hunt che mostra le schede delle azioni di invio e delle azioni di monitoraggio" /></td>
    </tr>
  </table>
</div>

---

## Ulteriori Letture

- [Creare una Shark Hunt](../how-to/create-shark-hunt.md) - guida passo dopo passo per creare la tua prima Hunt
