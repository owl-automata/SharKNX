# Come Connettersi a un Gateway KNX

SharKNX si connette alla tua installazione KNX tramite un gateway KNXnet/IP presente sulla rete locale. Questa guida illustra come rilevare automaticamente un gateway, salvarlo per un rapido riutilizzo, aggiungerne uno manualmente e stabilire la connessione.

---

## Opzione A - Scansione e Connessione (Scelta Consigliata al Primo Utilizzo)

1. Vai alla pagina **Discovery** e apri la scheda **Discover**.
2. Tocca il **FAB di scansione** (icona del radar). L'applicazione invierà richieste di rilevamento KNXnet/IP sulla rete locale ed elencherà tutti i gateway che rispondono.
3. Individua il tuo gateway tra i risultati. Ciascuna scheda mostra il nome del gateway, l'indirizzo IP, la porta e il supporto o meno a KNX IP Secure.
4. Tocca **Select** sulla scheda del gateway per impostarlo come gateway attivo per la sessione corrente.
   - Per salvarlo per le sessioni future, tocca **Save** sulla scheda. I gateway salvati appariranno nella scheda **Config** e potranno essere selezionati senza dover eseguire nuovamente la scansione.
5. Naviga fino alla pagina **Monitor** (o a qualsiasi pagina che richieda una connessione) e tocca il **FAB di avvio/connessione**. SharKNX si connetterà automaticamente al gateway selezionato.

> **Ultimo Gateway Selezionato:** L'ultimo gateway utilizzato viene memorizzato e mostrato in cima alla finestra a comparsa della connessione nelle pagine Monitor e Shark Hunt. Ciò significa che, dopo la prima configurazione, di norma non sarà più necessario visitare nuovamente la pagina Discovery.

---

## Opzione B - Aggiungere un Gateway Manualmente

Utilizza questa opzione quando il gateway si trova su una sottorete differente o non è rilevabile tramite multicast (ad esempio in caso di accesso remoto tramite VPN).

1. Vai alla pagina **Discovery** e apri la scheda **Config**.
2. Tocca il **FAB "+"** per aprire il modulo di inserimento manuale del gateway.
3. Compila i campi richiesti:

   | Campo | Descrizione |
   |---|---|
   | **Name** | Un'etichetta per identificare questo gateway nell'elenco |
   | **IP address** | L'indirizzo IPv4 del gateway |
   | **Port** | Valore predefinito: `3671` |
   | **Use KNX IP Secure** | Abilita se il gateway richiede un tunnel protetto |
   | **NAT mode** | Abilita se la connessione avviene tramite un router NAT o un firewall |

4. Tocca **Save**. Il gateway apparirà nell'elenco della scheda Config e sarà immediatamente disponibile per la selezione.
5. Tocca la voce del gateway per selezionarlo, quindi avvia il monitor o connettiti da una pagina di hunt.

> La scheda Config supporta fino a un massimo di **50** gateway salvati.

---

## Opzione C - Connessione tramite Multicast (Routing KNX IP)

Se la tua installazione utilizza un router KNX IP in modalità routing, SharKNX può ricevere e inviare comandi direttamente sul gruppo multicast, anziché instaurare un tunnel verso uno specifico gateway.

1. Vai alla pagina **Discovery** → scheda **Discover**.
2. Se durante la scansione non viene rilevato alcun router con funzionalità di routing, la sezione multicast potrebbe non apparire di default. Abilita l'opzione **Always show multicast options** in **Settings → Discover** per renderla visibile in modo permanente.
3. Tocca **Select** sull'opzione multicast. Non è richiesta alcuna configurazione di indirizzo IP o porta - l'app utilizzerà l'indirizzo e la porta multicast configurati in Settings → Discover (valori predefiniti: `224.0.23.12`, porta `3671`).

---

## Connessione con KNX IP Secure

Se il gateway richiede la modalità KNX IP Secure, carica le tue credenziali nella scheda **Security** della pagina Discovery prima di effettuare la connessione. Vedi [Configurare KNX IP Secure](setup-knx-ip-secure.md).

---

## Risoluzione dei Problemi

| Sintomo | Causa Probabile |
|---|---|
| Nessun gateway trovato dopo la scansione | Il dispositivo mobile e il gateway si trovano su sottoreti diverse, oppure il traffico multicast è bloccato - prova ad attivare **Force unicast subnet scan** in Settings → Discover, o aggiungi il gateway manualmente |
| Connessione in timeout | L'indirizzo IP o la porta del gateway sono errati, oppure il gateway è occupato con un altro client (la maggior parte dei gateway supporta un solo tunnel alla volta) |
| Connessione sicura fallita | Credenziali non caricate o keystore errato - verifica nuovamente la scheda Security |
| Gateway trovato ma non selezionabile | Il gateway potrebbe richiedere la modalità KNX IP Secure e le relative credenziali non sono ancora state caricate |
