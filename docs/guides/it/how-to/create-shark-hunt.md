# Come Creare una Shark Hunt

Una "shark hunt" è un set riutilizzabile di azioni di invio e filtri di monitoraggio salvati all'interno di un file portatile. Questa guida illustra la procedura guidata (wizard) di creazione in cinque passaggi e spiega come configurare ciascuna delle sei tipologie di azione disponibili.

Per una panoramica generale su cosa siano le shark hunts e su come funzioni la pagina di dettaglio, vedi [Shark Hunts](../concepts/shark-hunts.md).

> L'applicazione supporta fino a un massimo di **25 hunt**. Ciascuna hunt supporta fino a **25 azioni**.

---

## La Procedura Guidata (Wizard) di Creazione

Nella pagina principale delle Shark Hunts, tocca il **FAB "+"** per aprire la procedura guidata.

Ogni passaggio del wizard presenta:
- Un **pulsante X** (in alto a sinistra) per chiudere - l'applicazione mostrerà un avviso in caso di modifiche non salvate.
- Pulsanti **Back / Next** (Indietro / Avanti) in basso per navigare tra i vari passaggi.
- Un **pulsante Save (Salva)** (in alto a destra) che appare non appena viene apportata una modifica, consentendo di salvare i progressi e uscire per terminare in un secondo momento.

---

### Passaggio 1 - Nome e Descrizione

Inserisci un **nome** per la hunt (obbligatorio) e una **descrizione** opzionale. Attiva l'opzione **Mark as favourite** se desideri che la hunt appaia in cima all'elenco quando applichi il filtro con la stella nella pagina principale.

---

### Passaggio 2 - Progetto ETS

Scegli se questa specifica hunt utilizzerà un progetto ETS:

| Opzione | Quando utilizzarla |
|---|---|
| **Use loaded ETS project** | Un progetto è già caricato - la hunt utilizzerà i suoi indirizzi di gruppo, i dispositivi e la struttura degli edifici per la creazione delle azioni e dei filtri di monitoraggio. |
| **Load a project** | Non è ancora stato caricato alcun progetto - apre il selettore di file per permetterti di caricarne uno al momento. |
| **Manual input** | Non hai a disposizione o non ti serve un progetto - gli indirizzi di gruppo dovranno essere digitati manualmente durante la creazione delle azioni. |

> **Nota:** Le tipologie di azione **Monitor Space** e **Monitor Device** richiedono obbligatoriamente un progetto ETS. Se salti la selezione del progetto in questo passaggio, queste due azioni non saranno disponibili nel Passaggio 3.

---

### Passaggio 3 - Azioni

In questa fase andrai a costruire il contenuto vero e proprio della hunt. Tocca **Add action** e scegli un tipo di azione dall'elenco. Vedi la sezione [Tipologie di Azione](#tipologie-di-azione) più in basso per tutti i dettagli relativi a ciascun tipo.

Le azioni create appariranno sotto forma di schede. Ogni scheda presenta le opzioni:
- **Edit** - riapre la configurazione dell'azione.
- **Copy** - duplica l'azione (molto utile per azioni simili con piccole differenze).
- **Delete** - rimuove l'azione.

Ripeti la procedura fino a quando non avrai aggiunto tutte le azioni necessarie.

---

### Passaggio 4 - Gateway (Opzionale)

Opzionalmente, puoi incorporare la configurazione di un gateway all'interno della hunt. Questo permette a chi riceve una hunt condivisa di connettersi senza dover rilevare o configurare autonomamente il gateway - una soluzione ideale per condividere file con utenti non esperti per attività di diagnostica remota.

Seleziona un gateway tra quelli già rilevati oppure tocca **Configure manually** per inserire direttamente un indirizzo IP e una porta. Questo passaggio può essere saltato completamente se non è richiesto un gateway integrato.

---

### Passaggio 5 - Revisione e Creazione

Un riepilogo di tutte le scelte effettuate. Controlla i dati e tocca **Create** per terminare. La hunt apparirà come scheda nella pagina principale.

---

## Tipologie di Azione

La pagina di creazione di ogni azione richiede un **nome dell'azione** (obbligatorio) e una **descrizione** opzionale. Il **FAB con la spunta** diventa attivo non appena tutti i campi obbligatori sono stati compilati; toccandolo, l'azione viene salvata e creata.

---

### Send Fixed (Invio Valore Fisso)

Invia un singolo valore fisso a uno specifico indirizzo di gruppo ogni volta che si tocca la scheda dell'azione.

1. Inserisci l'indirizzo di gruppo, oppure tocca l'**icona di ricerca** per selezionarne uno dal progetto ETS caricato (procedura che precompila automaticamente il DPT).
2. Scegli **Write (Scrittura)** o **Read (Lettura)**.
3. Seleziona il tipo e il sottotipo di **DPT**.
4. Per la Scrittura: inserisci il valore da inviare (es. On, 75%, 21.5°C, Scenario 3).
5. Tocca il **FAB con la spunta** per salvare.

**Esempi:** Accendere/spegnere una luce, impostare il setpoint di un termostato, richiamare uno scenario, testare la posizione di una tapparelle.

---

### Send Multiple / Sequence (Invio Multiplo / Sequenza)

Invia un elenco di comandi fissi in sequenza, con la possibilità di inserire ritardi temporali (delay) tra l'uno e l'altro.

1. Tocca il **pulsante +** per aggiungere il primo comando - si aprirà il compositore di comandi. Inserisci l'indirizzo di gruppo, il DPT, l'operazione di lettura/scrittura e il valore, quindi tocca il FAB con la spunta per aggiungerlo.
2. Tocca nuovamente **+** per aggiungere altri comandi (fino a un massimo di **15**).
3. Ogni comando appare come una scheda espandibile che mostra il DPT e il valore associato.
4. Per inserire un ritardo prima di un comando: tocca il sottotitolo **"Immediate"** sulla scheda e inserisci il ritardo espresso in secondi (massimo **10 s**). Il comando successivo attenderà quel lasso di tempo prima di essere eseguito.
5. Per riordinare i comandi: tocca la **maniglia di trascinamento a sei punti** presente su una scheda e trascinala nella posizione desiderata.
6. Tocca il **FAB con la spunta** per salvare l'azione.

**Esempio:** Impostazione scenario → attendi 2 s → lettura stato → attendi 1 s → invio conferma.

---

### Send Variable (Invio Valore Variabile)

Invia un valore scelto al momento dell'esecuzione a uno o più indirizzi di gruppo. Questa funzione è utile quando è necessario testare valori differenti sullo stesso indirizzo o inviare un comando in broadcast a diversi indirizzi correlati contemporaneamente.

1. Inserisci un indirizzo di gruppo nel campo di input e tocca **Add**. Ripeti l'operazione per ogni indirizzo di destinazione (fino a un massimo di **15**).
   - Utilizza la **ricerca di progetto** per selezionare e includere contemporaneamente più indirizzi di gruppo dal progetto ETS caricato.
2. Tutti gli indirizzi inseriti devono condividere lo stesso DPT. Eventuali incongruenze verranno evidenziate sulle schede degli indirizzi ma non bloccheranno la creazione - tieni solo presente che i dispositivi potrebbero non rispondere come previsto.
3. Tocca il **FAB con la spunta** per salvare.

Quando eseguirai questa azione nella pagina della hunt, si aprirà una schermata inferiore con un'interfaccia di input adeguata al DPT. Inserisci il valore desiderato e conferma per inviarlo a tutti gli indirizzi di destinazione.

**Esempi:** Selezionare tutti gli indirizzi di gruppo dei setpoint dei termostati di un piano e inviare "21 °C" con un solo tocco per verificare che ogni zona HVAC risponda correttamente. Oppure associare tutti gli indirizzi dei canali dimmer di una stanza e scorrere i valori di luminosità per individuare quale livello causi sfarfallio (flicker).

---

### Custom Monitor (Monitor Personalizzato)

Crea un filtro avanzato per una sessione di monitoraggio utilizzando una o più condizioni combinate con la logica AND / OR.

1. Tocca il **pulsante +** per aggiungere una condizione. È possibile inserire fino a **10 condizioni**.
2. Scegli il tipo di condizione:

   | Condizione | Cosa filtra |
   |---|---|
   | **Group address** | Mostra solo i telegrammi da/verso specifici indirizzi di gruppo. Inserisci gli indirizzi manualmente o selezionali dal progetto. Supporta i caratteri jolly ovvero le wildcard (`1/*/*`, `1/*/0`). Attiva **Exclude** per invertire il filtro (mostra tutto tranne questi indirizzi). |
   | **Device address** | Mostra solo i telegrammi provenienti da specifici indirizzi individuali. Inserimento manuale o ricerca da progetto. Supporta i caratteri jolly (`1.*.*`). Attiva **Exclude** per invertire il filtro. |
   | **Telegram type** | Filtra per tipo APCI: Scrittura (Write), Lettura (Read), Risposta (Response) o qualsiasi combinazione di essi. |
   | **Text search** | Mostra solo i telegrammi il cui nome dell'indirizzo di gruppo o la cui descrizione contiene una determinata stringa di testo. Richiede un progetto ETS caricato. |
   | **Timestamp** | Mostra i telegrammi ricevuti prima, dopo o tra orari specifici. Ideale per testare automazioni basate su funzioni orarie. |

3. Dopo aver aggiunto le condizioni, imposta l'**operatore logico** di collegamento: **AND** (tutte le condizioni devono essere soddisfatte) o **OR** (è sufficiente che una sola condizione sia soddisfatta).
4. Tocca il **FAB con la spunta** per salvare.

**Esempi:**
- *Isolare un dispositivo sospetto:* Aggiungi una condizione "Device Address" inserendo il mittente sospetto AND una condizione "Group Address" inserendo l'intervallo di GA interessate. Verranno visualizzati solo i telegrammi inviati da quel dispositivo a quegli indirizzi - tutto il resto verrà filtrato.
- *Verificare un'automazione mattutina:* Aggiungi una condizione "Timestamp" (dopo le 07:00) AND una condizione "Telegram Type" (solo Write). Avvia il monitor il mattino seguente e verifica che lo schedulatore abbia inviato i comandi corretti all'orario stabilito.
- *Monitorare tutto escludendo il proprio traffico di test:* Aggiungi una condizione "Device Address" con l'opzione **Exclude** impostata sull'indirizzo individuale del tuo laptop o del tuo smartphone, in modo da visualizzare solo il reale traffico dell'impianto mentre effettui i test.

---

### Monitor Space (Monitoraggio Spazio/Locale)

Consente di creare rapidamente un filtro di monitoraggio circoscritto a uno spazio fisico presente nella struttura degli edifici del tuo progetto ETS. Richiede un progetto ETS (configurato nel Passaggio 2).

1. Scegli cosa monitorare:
   - **Group addresses** - monitora tutti gli indirizzi di gruppo assegnati ai dispositivi presenti nello spazio selezionato.
   - **Device senders** - monitora tutti gli indirizzi individuali dei dispositivi presenti nello spazio selezionato.
2. Tocca **Select space** - la struttura degli edifici del progetto ETS apparirà sotto forma di schermata. Seleziona un piano, una stanza o una qualsiasi area (es. Cucina, Soggiorno).
3. Tocca il **FAB con la spunta** per salvare.

> È possibile catturare fino a un massimo di **750 indirizzi** da una singola selezione di spazio. Spazi di grandi dimensioni con molti dispositivi potrebbero avvicinarsi a questo limite.

---

### Monitor Device (Monitoraggio Dispositivo)

Crea un filtro di monitoraggio circoscritto a uno o più dispositivi specifici del tuo progetto ETS. Richiega un progetto ETS (configurato nel Passaggio 2).

1. Tocca **Select devices** - apparirà l'elenco dei dispositivi del tuo progetto. Seleziona uno o più dispositivi.
2. Il filtro monitorerà tutti gli indirizzi di gruppo collegati ai dispositivi selezionati.
3. Tocca il **FAB con la spunta** per salvare.

> Si applica il medesimo limite di **750 indirizzi**. Molto utile per testare la comunicazione tra due dispositivi specifici o per verificare tutte le uscite di un attuatore/controllore.

---

## Modificare una Hunt Esistente

Dalla pagina principale, tocca il **menu a tre punti** sulla scheda di una qualsiasi hunt e seleziona **Edit**. Verrà riaperta la procedura guidata con tutti i dati precompilati. Potrai modificare il nome, aggiungere o rimuovere azioni, cambiare il gateway o aggiornare qualsiasi altra impostazione.

---

## Condividere una Hunt

Dal menu a tre punti, tocca **Share** per inviare la hunt sotto forma di file JSON tramite i canali di sistema (email, app di messaggistica, cloud drive). Il destinatario potrà importarla utilizzando l'opzione **icona delle regolazioni → Import Hunts** nella propria pagina delle Shark Hunts. Un singolo file esportato può contenere una o più hunt.
