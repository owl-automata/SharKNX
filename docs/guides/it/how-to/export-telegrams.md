# Come Esportare i Telegrammi

SharKNX consente di esportare in un file i telegrammi attualmente presenti nell'elenco di monitoraggio. È possibile scegliere quali colonne includere, il numero di telegrammi da considerare, lo stile dell'intestazione delle colonne e il formato del delimitatore. I file esportati possono essere salvati localmente o condivisi direttamente dall'applicazione.

---

## Dalla Pagina Monitor

1. Avvia una sessione di monitoraggio e attendi che i telegrammi si accumulino, oppure arresta il monitor una volta catturato il traffico di tuo interesse.
2. Tocca l'**icona di esportazione** (in alto a destra nella riga della barra dei filtri) per aprire la schermata di esportazione.
3. Configura le opzioni di esportazione:

   | Opzione | Descrizione |
   |---|---|
   | **File name (Nome file)** | Precompilato automaticamente con un timestamp. Modificalo per assegnare un nome significativo al file. |
   | **Columns (Colonne)** | Seleziona le caselle delle colonne da includere: ID, Time (Tempo), Source (Sorgente), Destination (Destinazione), Name\* (Nome), Type (Tipo), Value\* (Valore), Raw (Dato grezzo) (\*richiede un progetto ETS caricato). |
   | **Number of telegrams** | Quantità di telegrammi da esportare (conteggiati a partire dal più recente). Utilizza questa opzione per limitare un buffer di grandi dimensioni alle ultime N voci. |
   | **Include column headers** | Attiva questa opzione per includere una riga di intestazione in cima al file CSV. |
   | **Delimiter (Delimitatore)** | Virgola (predefinito), Tabulazione o Punto e virgola. |

4. Tocca **Save (Salva)** per salvare il file sul tuo dispositivo, oppure **Share (Condividi)** per aprire la schermata di condivisione di sistema e inviarlo direttamente via email, su un servizio di cloud storage o a un'altra applicazione.

---

## Dallo Shark Hunt Monitor

La medesima schermata di esportazione è disponibile all'interno di una sessione di monitoraggio di una Shark Hunt. Tocca il **pulsante di salvataggio/esportazione** nella barra superiore (attivo quando sono presenti telegrammi). Si applicano esattamente le stesse opzioni descritte sopra.

---

## Note Importanti

- Le colonne **Name** e **Value** sono significative solo se è presente un progetto ETS caricato. Senza un progetto, queste colonne risulteranno vuote per la maggior parte dei telegrammi.
- La colonna **Raw** è sempre disponibile e contiene il payload esadecimale non analizzato - questo rappresenta il dato reale ("ground truth") che l'applicazione converte in un valore leggibile dall'utente quando viene caricato un progetto.
- L'esportazione acquisisce tutto ciò che è attualmente presente nel buffer dei telegrammi. Se il buffer ha raggiunto il suo limite massimo (valore predefinito 2000, modificabile in **Settings → Monitor**), i telegrammi più vecchi saranno già stati sovrascritti. Se hai la necessità di effettuare un'acquisizione prolungata, esegui l'esportazione prima che il buffer si riempia.
- I file esportati possono essere nuovamente importati nel monitor per essere analizzati. Dal **menu di ottimizzazione (tune menu) di Monitor**, utilizza la funzione **Import CSV** per ricaricare un file precedentemente esportato all'interno dell'elenco dei telegrammi.
