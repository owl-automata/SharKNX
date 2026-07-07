# Tipi di Datapoint Supportati (DPT)

SharKNX supporta i tipi di datapoint KNX (DPT) in due ambiti differenti:

- **Decodifica** - i valori vengono decodificati e visualizzati alla ricezione dei telegrammi all'interno del Monitor. Si applica a tutti i DPT elencati in questo documento.
- **Invio** - i DPT selezionabili durante la composizione di un comando. Rappresentano un sottoinsieme dei DPT decodificabili e sono contrassegnati con il simbolo ✅ nella tabella sottostante.

Se viene ricevuto un telegramma destinato a un indirizzo di gruppo il cui DPT è sconosciuto o non ancora supportato, verrà mostrato il payload grezzo in formato esadecimale (raw hex) al posto del valore decodificato.

---

## Panoramica

| DPT | Nome | Dimensione | Invio |
|-----|------|------|------|
| **1** | 1-bit Booleano | 1 bit | ✅ |
| **2** | 1-bit Controllato | 2 bit | ✅ |
| **3** | 3-bit Controllato (Step) | 4 bit | ✅ |
| **4** | Carattere | 1 byte | ✅ |
| **5** | Valore Non Segnato a 8-bit | 1 byte | ✅ |
| **6** | Valore Segnato a 8-bit | 1 byte | ✅ |
| **7** | Valore Non Segnato a 2-byte | 2 byte | ✅ |
| **8** | Valore Segnato a 2-byte | 2 byte | ✅ |
| **9** | Float a 2-byte | 2 byte | ✅ |
| **10** | Ora del Giorno (Time of Day) | 3 byte | ✅ |
| **11** | Data | 3 bytes | ✅ |
| **12** | Valore Non Segnato a 4-byte | 4 byte | ✅ |
| **13** | Valore Segnato a 4-byte | 4 byte | ✅ |
| **14** | Float IEEE 754 a 4-byte | 4 byte | ✅ |
| **15** | Controllo Accessi (Entrance Access) | 4 byte | - |
| **16** | Stringa a 14 Caratteri | 14 byte | ✅ |
| **17** | Numero Scenario | 1 byte | ✅ |
| **18** | Controllo Scenario | 1 byte | ✅ |
| **19** | Data e Ora | 8 byte | ✅ |
| **20** | Enum a 1-byte | 1 byte | ✅ |
| **21** | Stato / Flag a 8-bit | 1 byte | ✅ |
| **22** | Stato / Flag a 16-bit | 2 byte | ✅ |
| **23** | Set a 2-bit | 1 byte | - |
| **24** | Stringa a Lunghezza Variabile (ISO 8859-1) | variabile | - |
| **25** | Double Nibble | 1 byte | - |
| **26** | Info Scenario | 1 byte | - |
| **27** | Info Combinata a 32-bit | 4 byte | - |
| **28** | Stringa a Lunghezza Variabile (UTF-8) | variabile | ✅ |
| **29** | Valore Segnato a 8-byte | 8 byte | ✅ |
| **30** | Attivazione Canale (24 ch) | 3 byte | - |
| **206** | Ritardo Temporale + Modalità HVAC | 3 byte | - |
| **217** | Versione | 2 byte | - |
| **219** | Info Allarme | 6 byte | - |
| **222** | Setpoint di Temperatura (×3) | 6 byte | - |
| **225** | Tempo di Step Scalatura | 4 byte | - |
| **229** | Valore di Misurazione (Metering) | 6 byte | - |
| **232** | Colore RGB | 3 byte | ✅ |
| **234** | Codice Lingua | 2 byte | - |
| **235** | Tariffa Energia Attiva | 6 byte | - |
| **240** | Posizione Combinata (tapparelle) | 3 byte | - |
| **241** | Stato Attuatore Tapparelle | 4 byte | - |
| **242** | Colore CIE xyY | 6 byte | ✅ |
| **243** | Transizione Colore xyY | 8 byte | - |
| **249** | Transizione Luminosità e CCT | 6 byte | ✅ |
| **250** | Controllo Luminosità e CCT (relativo) | 3 byte | ✅ |
| **251** | Colore RGBW | 6 byte | ✅ |
| **252** | Controllo Relativo RGBW | 5 byte | ✅ |
| **253** | Controllo Relativo xyY | 4 byte | - |
| **254** | Controllo Relativo RGB | 3 byte | ✅ |
| **275** | Quattro Float a 2-byte | 8 byte | - |

---

## Sottotipi

Le sezioni seguenti elencano i sottotipi selezionabili in fase di **invio** dei comandi, raggruppati per tipo principale. I DPT dotati di un singolo sottotipo o privi del supporto all'invio manuale sono stati omessi.

### DPT 1 - 1-bit Booleano

| Sottotipo | Descrizione |
|---------|-------------|
| 1.001 | Interruttore (On / Off) |
| 1.002 | Booleano |
| 1.003 | Abilitazione |
| 1.004 | Rampa |
| 1.005 | Allarme |
| 1.006 | Valore Binario |
| 1.007 | Step |
| 1.008 | Su / Giù (Up / Down) |
| 1.009 | Apri / Chiudi |
| 1.010 | Avvio / Arresto (Start / Stop) |
| 1.011 | Stato |
| 1.012 | Inversione |
| 1.013 | Stile Invio Dimmer |
| 1.014 | Sorgente Ingresso |
| 1.015 | Ripristino (Reset) |
| 1.016 | Conferma (Acknowledge) |
| 1.017 | Attivazione (Trigger) |
| 1.018 | Presenza / Occupazione |
| 1.019 | Finestra / Porta |
| 1.021 | Funzione Logica |
| 1.022 | Scenario A/B |
| 1.023 | Modalità Veneziane / Tapparelle |
| 1.100 | Raffrescamento / Riscaldamento |

### DPT 2 - 1-bit Controllato

| Sottotipo | Descrizione |
|---------|-------------|
| 2.001 | Controllo Interruttore |
| 2.002 | Controllo Booleano |
| 2.003 | Controllo Abilitazione |
| 2.004 | Controllo Rampa |
| 2.005 | Controllo Allarme |
| 2.006 | Controllo Valore Binario |
| 2.007 | Controllo Step |
| 2.008 | Controllo Direzione 1 |
| 2.009 | Controllo Direzione 2 |
| 2.010 | Controllo Avvio |
| 2.011 | Controllo Stato |
| 2.012 | Controllo Inversione |

### DPT 3 - 3-bit Controllato

| Sottotipo | Descrizione |
|---------|-------------|
| 3.007 | Controllo Dimmerazione |
| 3.008 | Controllo Tapparelle |

### DPT 4 - Carattere

| Sottotipo | Descrizione |
|---------|-------------|
| 4.001 | Carattere (ASCII) |
| 4.002 | Carattere (ISO 8859-1) |

### DPT 5 - Valore Non Segnato a 8-bit

| Sottotipo | Descrizione | Intervallo | Unità |
|---------|-------------|-------|------|
| 5.001 | Scalatura / Percentuale | 0-100 | % |
| 5.003 | Angolo | 0-360 | ° |
| 5.004 | Percentuale | 0-255 | % |
| 5.005 | Rapporto (Ratio) | 0-255 | - |
| 5.006 | Tariffa | 0-255 | - |
| 5.010 | Conteggio Impulsi | 0-255 | - |

### DPT 6 - Valore Segnato a 8-bit

| Sottotipo | Descrizione | Intervallo | Unità |
|---------|-------------|-------|------|
| 6.001 | Percentuale | -128-127 | % |
| 6.010 | Conteggio Impulsi | -128-127 | - |

### DPT 7 - Valore Non Segnato a 2-byte

| Sottotipo | Descrizione | Unità |
|---------|-------------|------|
| 7.001 | Impulsi | - |
| 7.002 | Periodo di Tempo | ms |
| 7.003 | Periodo di Tempo | 10 ms |
| 7.004 | Periodo di Tempo | 100 ms |
| 7.005 | Periodo di Tempo | s |
| 7.006 | Periodo di Tempo | min |
| 7.007 | Periodo di Tempo | h |
| 7.011 | Lunghezza | mm |
| 7.012 | Corrente | mA |
| 7.013 | Luminosità | lux |
| 7.600 | Temperatura Colore | K |

### DPT 8 - Valore Segnato a 2-byte

| Sottotipo | Descrizione | Unità |
|---------|-------------|------|
| 8.001 | Differenza Impulsi | - |
| 8.002 | Ritardo Temporale | ms |
| 8.003 | Ritardo Temporale | 10 ms |
| 8.004 | Ritardo Temporale | 100 ms |
| 8.005 | Ritardo Temporale | s |
| 8.006 | Ritardo Temporale | min |
| 8.007 | Ritardo Temporale | h |
| 8.010 | Differenza Percentuale | % |
| 8.011 | Angolo di Rotazione | ° |

### DPT 9 - Float a 2-byte

| Sottotipo | Descrizione | Unità |
|---------|-------------|------|
| 9.001 | Temperatura | °C |
| 9.002 | Differenza di Temperatura | K |
| 9.003 | Variazione di Temperatura | K/h |
| 9.004 | Illuminamento | lux |
| 9.005 | Velocità del Vento | m/s |
| 9.006 | Pressione | Pa |
| 9.007 | Umidità | % |
| 9.008 | Qualità dell'Aria (CO₂) | ppm |
| 9.009 | Portata d'Aria | m³/h |
| 9.010 | Tempo | s |
| 9.011 | Tempo | ms |
| 9.020 | Tensione | mV |
| 9.021 | Corrente | mA |
| 9.022 | Densità di Potenza | W/m² |
| 9.023 | Kelvin per Percento | K/% |
| 9.024 | Potenza | kW |
| 9.025 | Portata Volumetrica | l/h |
| 9.026 | Quantità di Pioggia | l/m² |
| 9.027 | Temperatura | °F |
| 9.028 | Velocità del Vento | km/h |

### DPT 13 - Valore Segnato a 4-byte

| Sottotipo | Descrizione | Unità |
|---------|-------------|------|
| 13.001 | Conteggio Impulsi | - |
| 13.002 | Portata | m³/h |
| 13.010 | Energia Attiva | Wh |
| 13.011 | Energia Apparente | VAh |
| 13.012 | Energia Reattiva | VARh |
| 13.013 | Energia Attiva | kWh |
| 13.014 | Energia Apparente | kVAh |
| 13.015 | Energia Reattiva | kVARh |
| 13.100 | Ritardo Temporale | s |

### DPT 14 - Float IEEE a 4-byte (sottotipi selezionati)

Solo un sottoinsieme degli 80 sottotipi del DPT 14 è disponibile nell'interfaccia utente di invio. Tutti i sottotipi vengono comunque decodificati correttamente nel monitor.

| Sottotipo | Descrizione | Unità |
|---------|-------------|------|
| 14.007 | Angolo | ° |
| 14.019 | Corrente Elettrica | A |
| 14.027 | Potenziale Elettrico | V |
| 14.033 | Frequenza | Hz |
| 14.056 | Potenza | W |
| 14.065 | Velocità | m/s |
| 14.068 | Temperatura | °C |
| 14.069 | Temperatura Assoluta | K |
| 14.070 | Differenza di Temperatura | K |

### DPT 16 - Stringa a 14 Caratteri

| Sottotipo | Descrizione |
|---------|-------------|
| 16.000 | ASCII |
| 16.001 | ISO 8859-1 |

### DPT 20 - Enum a 1-byte

| Sottotipo | Descrizione |
|---------|-------------|
| 20.002 | Modalità Edificio (Building Mode) |
| 20.003 | Modalità Occupato |
| 20.004 | Priorità |
| 20.005 | Modalità Applicazione Illuminazione |
| 20.006 | Area Applicazione Illuminazione |
| 20.007 | Tipo Classe Allarme |
| 20.008 | Modalità Alimentatore (PSU Mode) |
| 20.013 | Ritardo Temporale |
| 20.014 | Forza del Vento (Beaufort) |
| 20.100 | Tipo di Combustibile |
| 20.101 | Tipo di Bruciatore |
| 20.102 | Modalità HVAC |
| 20.103 | Modalità ACS (DHW Mode) |
| 20.104 | Priorità Carico |
| 20.105 | Modalità Controllo HVAC |
| 20.106 | Modalità Emergenza HVAC |
| 20.107 | Modalità Commutazione (Changeover) |
| 20.108 | Modalità Valvola |
| 20.109 | Modalità Serranda (Damper Mode) |
| 20.110 | Modalità Riscaldatore |
| 20.111 | Modalità Ventilatore |
| 20.112 | Modalità Master / Slave |
| 20.113 | Stato Setpoint Ambiente |

> **Nota:** La visualizzazione delle etichette descrittive per la maggior parte dei sottotipi DPT 20 mostra come fallback il valore numerico grezzo. Le descrizioni testuali (es. "Comfort", "Standby") sono attive per il tipo 20.102 (Modalità HVAC) e pochi altri sottotipi.

### DPT 21 - Flag di Stato a 8-bit

| Sottotipo | Descrizione |
|---------|-------------|
| 21.001 | Stato Generale |
| 21.002 | Controllo Dispositivo |
| 21.100 | Segnale di Forzamento |
| 21.102 | Stato Regolatore Riscaldamento Ambiente |
| 21.103 | Stato Regolatore Solare ACS |
| 21.105 | Stato Regolatore Raffrescamento Ambiente |
| 21.106 | Stato Regolatore Ventilazione |

### DPT 22 - Flag di Stato a 16-bit

| Sottotipo | Descrizione |
|---------|-------------|
| 22.100 | Stato Regolatore ACS |
| 22.101 | Stato RHCC |

### DPT 29 - Valore Segnato a 8-byte (Energia a 64-bit)

| Sottotipo | Descrizione | Unità |
|---------|-------------|------|
| 29.010 | Energia Attiva | Wh |
| 29.011 | Energia Apparente | VAh |
| 29.012 | Energia Reattiva | VARh |

### DPT 232 / 242 / 249 / 250 / 251 / 252 / 254 - Illuminazione e Colore

| DPT | Descrizione | Dimensione |
|-----|-------------|------|
| 232.600 | Colore RGB | 3 byte |
| 242.600 | Colore CIE xyY | 6 byte |
| 249.600 | Transizione Luminosità e Temperatura Colore | 6 byte |
| 250.600 | Controllo Luminosità e Temperatura Colore (relativo) | 3 byte |
| 251.600 | Colore RGBW | 6 byte |
| 252.600 | Controllo Relativo RGBW | 5 byte |
| 254.600 | Controllo Relativo RGB | 3 byte |

---

## DPT Sola Decodifica (Decode-only)

I seguenti DPT vengono decodificati all'interno del monitor solo quando il progetto ETS fornisce l'assegnazione corretta del datapoint, ma non sono disponibili per la composizione manuale dei comandi nell'interfaccia utente di invio.

| DPT | Descrizione |
|-----|-------------|
| 15.000 | Controllo Accessi (codice di accesso) |
| 23.x | Set Azioni a 2-bit (on/off, su/giù, allarme) |
| 24.x | Stringa a Lunghezza Variabile (ISO 8859-1) |
| 25.x | Double Nibble |
| 26.001 | Info Scenario |
| 27.001 | Info Bit-combinata On/Off |
| 30.1010 | Attivazione Canale (24 canali) |
| 206.x | Ritardo Temporale + Modalità HVAC/ACS/Presenza/Edificio |
| 217.001 | Versione DPT |
| 219.001 | Info Allarme |
| 222.x | Setpoint di Temperatura Ambiente (×3) |
| 225.x | Tempo di Step Scalatura |
| 229.001 | Valore di Misurazione (Metering) |
| 234.001 | Codice Lingua (ISO 639-1) |
| 235.001 | Tariffa Energia Attiva |
| 240.800 | Posizione Combinata (veneziane/tapparelle) |
| 241.800 | Stato Attuatore Tapparelle |
| 243.x | Transizione Colore xyY |
| 253.x | Controllo Relativo xyY |
| 275.x | Quattro Float a 2-byte |
