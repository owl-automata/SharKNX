# Come Scansionare una Linea Bus KNX

La scansione di una linea bus esamina a fondo ogni singolo indirizzo individuale su una linea KNX ed elenca tutti i dispositivi che rispondono. Questo ti permette di verificare cosa sia realmente installato - indipendentemente da qualsiasi progetto ETS - e rappresenta il modo più rapido per ottenere una panoramica di un impianto sconosciuto.

---

## Prerequisiti

- Connessione a un gateway KNX attiva (vedi [Connettersi a un Gateway](connect-to-gateway.md)).
- Conoscere il numero di area e di linea KNX che si desidera scansionare (es. area 1, linea 1 → `1.1`).

---

## Passaggi

1. Vai a **Management → scheda Line Scan**.
2. Nella scheda **Scan Settings (Impostazioni Scansione)**, configura i parametri:

   | Impostazione | Descrizione |
   |---|---|
   | **Area / Line** | L'area e la linea da scansionare (es. `1.1`). Tocca **Choose from project** per selezionare una linea dal tuo progetto ETS caricato - questa operazione imposta automaticamente anche il tipo di mezzo trasmissivo (medium). |
   | **Medium type** | Il mezzo trasmissivo della linea: TP (doppino intrecciato), IP o IoT. Deve corrispondere al mezzo fisico della linea. |
   | **Range** | L'indirizzo iniziale e finale del dispositivo all'interno della linea (0–255). Riduci questo intervallo per velocizzare la scansione o controllare un segmento specifico. |

3. Tocca il **FAB di scansione** per iniziare. La scansione può essere interrotta in qualsiasi momento.
4. I dispositivi rilevati appariranno sotto forma di schede. Il colore del bordo superiore indica il tipo di dispositivo:

   | Colore | Tipo |
   |---|---|
   | Blu | Accoppiatore KNX (linea/area) |
   | Rosso | Dispositivo applicativo standard |
   | Verde | Dispositivo KNX Secure |

---

## Lettura delle Info Dispositivo per Tutti i Dispositivi Rilevati

Al termine della scansione, tocca **Read Device Info** (sopra l'elenco delle schede). L'applicazione leggerà in sequenza il produttore, il numero di serie e altri dettagli per ciascun dispositivo rilevato.

Questa funzione è utile per:
- Creare rapidamente un inventario di un impianto di cui non si è curata la messa in servizio.
- Effettuare un riscontro incrociato con un progetto ETS per verificare che corrisponda all'installazione fisica reale.
- Individuare dispositivi con indirizzi o tipologie impreviste.

---

## Lavorare con le Singole Schede dei Dispositivi

Tocca una scheda qualsiasi per aprire la sua schermata dei dettagli. Da lì puoi eseguire le seguenti operazioni:

- **Check** - verifica se il dispositivo risponde ancora sul bus.
- **Read Info** - legge i dettagli completi del dispositivo (produttore, firmware, stato di esecuzione, ecc.).
- **Toggle Programming Mode** - attiva o disattiva da remoto la modalità di programmazione del dispositivo.
- **Restart** - invia un comando di riavvio (reset software).
- **Program Address** - assegna un nuovo indirizzo individuale (vedi [Programmare l'Indirizzo Individuale di un Dispositivo](program-device-address.md)).
- **Rebuild Communication** - apre la scheda Inspect con l'indirizzo di questo dispositivo già precompilato per leggerne le tabelle di comunicazione.

---

## Esportazione dei Risultati della Scansione

Tocca l'**icona delle regolazioni (tune icon)** nella barra superiore per esportare il risultato dell'ultima scansione effettuata:
- **Export as text** - report in formato TXT contenente il timestamp della scansione, il gateway utilizzato, l'area/linea, il mezzo trasmissivo e l'elenco dei dispositivi.
- **Export as PDF** - gli stessi contenuti formattati in un documento PDF.
