# Come Caricare un Progetto ETS

Il caricamento di un file `.knxproj` fornisce a SharKNX l'accesso ai nomi degli indirizzi di gruppo, ai tipi di datapoint (DPT), ai metadati dei dispositivi e alle chiavi di sicurezza KNX Data Secure. Senza un progetto caricato, il monitor mostrerà esclusivamente i valori esadecimali grezzi (raw hex) senza alcuna descrizione.

---

## Prima di Iniziare

Il file `.knxproj` deve essere già presente sul tuo dispositivo mobile. Se non lo è, trasferiscilo preventivamente seguendo uno di questi metodi:
- Condividilo direttamente da ETS verso il telefono tramite un'app di messaggistica, email o AirDrop.
- Salvalo su un servizio di cloud storage (iCloud, Google Drive, OneDrive) e aprilo da lì.
- Trasferiscilo tramite cavo USB.

SharKNX supporta i file `.knxproj` generati da **ETS5 ed ETS6**, inclusi i progetti protetti da password.

---

## Passaggi

1. Vai alla pagina **Project** (la seconda scheda nella navigazione inferiore).
2. Tocca il **FAB della cartella**.
   - Se hai già caricato dei progetti in precedenza, si aprirà una **schermata con la cronologia**. Tocca una qualsiasi voce per ricaricare istantaneamente quel progetto, senza dover sfogliare nuovamente i file.
   - Per caricare un nuovo file, tocca **Browse (Sfoglia)** (o il pulsante del selettore di file) per aprire il selettore di file del sistema operativo.
3. Seleziona il tuo file `.knxproj`.
4. Se il progetto è **protetto da password**, inserisci la password quando richiesto e conferma.
5. Il progetto viene caricato. La barra di ricerca, il pulsante espandi/comprimi e le quattro schede (Group Addresses, Devices, Topology, Buildings) diventano immediatamente attivi.

---

## Cosa Cambia Dopo il Caricamento

- La **pagina Monitor** e lo **Shark Hunt monitor** mostreranno ora i nomi degli indirizzi di gruppo e i valori decodificati per tutti i telegrammi in ingresso.
- La barra di ricerca della **pagina Project** ti permette di filtrare per nome tutti gli indirizzi di gruppo, i dispositivi e gli elementi della struttura edilizia.
- Se il progetto contiene indirizzi di gruppo **KNX Data Secure**, apparirà un banner al di sotto della barra delle schede. Toccalo per configurare gli indirizzi dei mittenti prima di inviare comandi protetti. Vedi [Configurare KNX Data Secure](setup-knx-data-secure.md).

---

## Caricamento da Altre Schermate

Non è obbligatorio navigare fino alla pagina Project per caricare un progetto. Il **badge ETS Project** presente nella pagina Monitor e nelle pagine delle Shark Hunt mostra un pulsante **Load project** quando non ci sono progetti attivi - toccandolo si apriranno la medesima schermata della cronologia e il selettore di file.

---

## Aggiornare o Sostituire un Progetto

SharKNX mantiene in memoria un solo progetto alla volta. Per passare a un'esportazione più recente o a un altro progetto:

1. Tocca nuovamente il **FAB della cartella** nella pagina Project (oppure il badge ETS Project in qualsiasi altra schermata dell'app).
2. Seleziona il file `.knxproj` aggiornato.
3. Il nuovo progetto sostituirà immediatamente quello precedente.

> Se il monitor è attivo nel momento in cui carichi un nuovo progetto, le modifiche verranno applicate ai nuovi telegrammi in ingresso. I telegrammi già presenti nell'elenco manterranno i metadati del progetto precedente finché l'elenco non verrà svuotato.

Per rimuovere completamente un progetto dalla memoria senza caricarne uno nuovo, tocca l'**icona delle regolazioni (tune icon)** nella pagina Project e seleziona **Unload project**.

---

## Note Importanti

- Il caricamento di un progetto errato (ovvero non corrispondente all'impianto fisico reale) comporterà la visualizzazione di nomi di indirizzi di gruppo e valori decodificati non corretti nel monitor. Verifica sempre di avere il progetto corretto per il cantiere su cui stai lavorando.
- Il file di progetto viene letto una sola volta al momento del caricamento. SharKNX non rimane connesso a ETS e non rileva le modifiche apportate su ETS dopo il caricamento del file. Ricarica il file dopo ogni modifica effettuata in ETS.
- SharKNX non modifica mai in alcun modo il file `.knxproj` originale.
