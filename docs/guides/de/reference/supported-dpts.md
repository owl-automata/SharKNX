# Unterstützte Datapoint Types (DPTs)

SharKNX unterstützt KNX Datapoint Types in zwei Kontexten:

- **Dekodierung** — Werte werden im Monitor automatisch dekodiert und angezeigt, sobald Telegramme empfangen werden. Dies gilt für alle in diesem Dokument aufgeführten DPTs.
- **Senden** — DPTs, die beim Erstellen eines Kommandos auswählbar sind. Dies ist eine Teilmenge der dekodierbaren DPTs und in der Tabelle unten mit ✅ markiert.

Wenn ein Telegramm für eine Gruppenadresse empfangen wird, deren DPT unbekannt oder noch nicht unterstützt ist, wird statt eines dekodierten Werts der rohe Hex-Payload angezeigt.

---

## Übersicht

| DPT | Name | Größe | Senden |
|-----|------|------|------|
| **1** | 1-Bit Boolean | 1 Bit | ✅ |
| **2** | 1-Bit Controlled | 2 Bit | ✅ |
| **3** | 3-Bit Controlled (Step) | 4 Bit | ✅ |
| **4** | Zeichen | 1 Byte | ✅ |
| **5** | 8-Bit Unsigned Value | 1 Byte | ✅ |
| **6** | 8-Bit Signed Value | 1 Byte | ✅ |
| **7** | 2-Byte Unsigned Value | 2 Byte | ✅ |
| **8** | 2-Byte Signed Value | 2 Byte | ✅ |
| **9** | 2-Byte Float | 2 Byte | ✅ |
| **10** | Uhrzeit | 3 Byte | ✅ |
| **11** | Datum | 3 Byte | ✅ |
| **12** | 4-Byte Unsigned Value | 4 Byte | ✅ |
| **13** | 4-Byte Signed Value | 4 Byte | ✅ |
| **14** | 4-Byte IEEE 754 Float | 4 Byte | ✅ |
| **15** | Entrance Access | 4 Byte | — |
| **16** | 14-Zeichen-String | 14 Byte | ✅ |
| **17** | Szenennummer | 1 Byte | ✅ |
| **18** | Szenensteuerung | 1 Byte | ✅ |
| **19** | Datum & Uhrzeit | 8 Byte | ✅ |
| **20** | 1-Byte Enum | 1 Byte | ✅ |
| **21** | 8-Bit Status / Flags | 1 Byte | ✅ |
| **22** | 16-Bit Status / Flags | 2 Byte | ✅ |
| **23** | 2-Bit Set | 1 Byte | — |
| **24** | Variabler String (ISO 8859-1) | variabel | — |
| **25** | Double Nibble | 1 Byte | — |
| **26** | Scene Info | 1 Byte | — |
| **27** | 32-Bit Combined Info | 4 Byte | — |
| **28** | Variabler String (UTF-8) | variabel | ✅ |
| **29** | 8-Byte Signed Value | 8 Byte | ✅ |
| **30** | Channel Activation (24 ch) | 3 Byte | — |
| **206** | Time Delay + HVAC Mode | 3 Byte | — |
| **217** | Version | 2 Byte | — |
| **219** | Alarm Info | 6 Byte | — |
| **222** | Temperatur-Sollwerte (×3) | 6 Byte | — |
| **225** | Scaling Step Time | 4 Byte | — |
| **229** | Metering Value | 6 Byte | — |
| **232** | RGB-Farbe | 3 Byte | ✅ |
| **234** | Sprachcode | 2 Byte | — |
| **235** | Tariff Active Energy | 6 Byte | — |
| **240** | Combined Position (Jalousien) | 3 Byte | — |
| **241** | Shutter Actuator Status | 4 Byte | — |
| **242** | CIE xyY Farbe | 6 Byte | ✅ |
| **243** | xyY Farb-Transition | 8 Byte | — |
| **249** | Helligkeit & CCT Transition | 6 Byte | ✅ |
| **250** | Helligkeit & CCT Control (relativ) | 3 Byte | ✅ |
| **251** | RGBW Farbe | 6 Byte | ✅ |
| **252** | Relative Control RGBW | 5 Byte | ✅ |
| **253** | Relative Control xyY | 4 Byte | — |
| **254** | Relative Control RGB | 3 Byte | ✅ |
| **275** | Vier 2-Byte Floats | 8 Byte | — |

---

## Subtypen

Die folgenden Abschnitte listen die beim **Senden** auswählbaren Subtypen, gruppiert nach Haupt-DPT. DPTs mit nur einem Subtyp oder ohne Sende-Unterstützung sind ausgelassen.

### DPT 1 — 1-Bit Boolean

| Subtyp | Beschreibung |
|---------|-------------|
| 1.001 | Schalten (Aus / Ein) |
| 1.002 | Boolean |
| 1.003 | Aktivieren |
| 1.004 | Ramp |
| 1.005 | Alarm |
| 1.006 | Binärwert |
| 1.007 | Step |
| 1.008 | Auf / Ab |
| 1.009 | Öffnen / Schließen |
| 1.010 | Start / Stopp |
| 1.011 | Zustand |
| 1.012 | Invertieren |
| 1.013 | Dim Send Style |
| 1.014 | Input Source |
| 1.015 | Reset |
| 1.016 | Quittierung |
| 1.017 | Trigger |
| 1.018 | Belegung |
| 1.019 | Fenster / Tür |
| 1.021 | Logische Funktion |
| 1.022 | Szene A/B |
| 1.023 | Jalousie-/Blind-Modus |
| 1.100 | Kühlen / Heizen |

### DPT 2 — 1-Bit Controlled

| Subtyp | Beschreibung |
|---------|-------------|
| 2.001 | Schaltsteuerung |
| 2.002 | Boolean Control |
| 2.003 | Enable Control |
| 2.004 | Ramp Control |
| 2.005 | Alarm Control |
| 2.006 | Binary Value Control |
| 2.007 | Step Control |
| 2.008 | Richtungssteuerung 1 |
| 2.009 | Richtungssteuerung 2 |
| 2.010 | Start Control |
| 2.011 | State Control |
| 2.012 | Invert Control |

### DPT 3 — 3-Bit Controlled

| Subtyp | Beschreibung |
|---------|-------------|
| 3.007 | Dimmsteuerung |
| 3.008 | Jalousiesteuerung |

### DPT 4 — Character

| Subtyp | Beschreibung |
|---------|-------------|
| 4.001 | Zeichen (ASCII) |
| 4.002 | Zeichen (ISO 8859-1) |

### DPT 5 — 8-Bit Unsigned

| Subtyp | Beschreibung | Bereich | Einheit |
|---------|-------------|--------|--------|
| 5.001 | Skalierung / Prozent | 0–100 | % |
| 5.003 | Winkel | 0–360 | ° |
| 5.004 | Prozentwert | 0–255 | % |
| 5.005 | Verhältnis | 0–255 | — |
| 5.006 | Tarif | 0–255 | — |
| 5.010 | Zählerimpulse | 0–255 | — |

### DPT 6 — 8-Bit Signed

| Subtyp | Beschreibung | Bereich | Einheit |
|---------|-------------|--------|--------|
| 6.001 | Prozentwert | −128–127 | % |
| 6.010 | Zählerimpulse | −128–127 | — |

### DPT 7 — 2-Byte Unsigned

| Subtyp | Beschreibung | Einheit |
|---------|-------------|--------|
| 7.001 | Impulse | — |
| 7.002 | Zeitdauer | ms |
| 7.003 | Zeitdauer | 10 ms |
| 7.004 | Zeitdauer | 100 ms |
| 7.005 | Zeitdauer | s |
| 7.006 | Zeitdauer | min |
| 7.007 | Zeitdauer | h |
| 7.011 | Länge | mm |
| 7.012 | Strom | mA |
| 7.013 | Helligkeit | lux |
| 7.600 | Farbtemperatur | K |

### DPT 8 — 2-Byte Signed

| Subtyp | Beschreibung | Einheit |
|---------|-------------|--------|
| 8.001 | Impulsdifferenz | — |
| 8.002 | Zeitversatz | ms |
| 8.003 | Zeitversatz | 10 ms |
| 8.004 | Zeitversatz | 100 ms |
| 8.005 | Zeitversatz | s |
| 8.006 | Zeitversatz | min |
| 8.007 | Zeitversatz | h |
| 8.010 | Prozentdifferenz | % |
| 8.011 | Drehwinkel | ° |

### DPT 9 — 2-Byte Float

| Subtyp | Beschreibung | Einheit |
|---------|-------------|--------|
| 9.001 | Temperatur | °C |
| 9.002 | Temperaturdifferenz | K |
| 9.003 | Temperaturänderung | K/h |
| 9.004 | Beleuchtungsstärke | lux |
| 9.005 | Windgeschwindigkeit | m/s |
| 9.006 | Druck | Pa |
| 9.007 | Luftfeuchtigkeit | % |
| 9.008 | Luftqualität (CO₂) | ppm |
| 9.009 | Luftstrom | m³/h |
| 9.010 | Zeit | s |
| 9.011 | Zeit | ms |
| 9.020 | Spannung | mV |
| 9.021 | Strom | mA |
| 9.022 | Leistungsdichte | W/m² |
| 9.023 | Kelvin pro Prozent | K/% |
| 9.024 | Leistung | kW |
| 9.025 | Volumenstrom | l/h |
| 9.026 | Regenmenge | l/m² |
| 9.027 | Temperatur | °F |
| 9.028 | Windgeschwindigkeit | km/h |

### DPT 13 — 4-Byte Signed

| Subtyp | Beschreibung | Einheit |
|---------|-------------|--------|
| 13.001 | Zählerimpulse | — |
| 13.002 | Durchflussrate | m³/h |
| 13.010 | Wirkenergie | Wh |
| 13.011 | Scheinenergie | VAh |
| 13.012 | Blindenergie | VARh |
| 13.013 | Wirkenergie | kWh |
| 13.014 | Scheinenergie | kVAh |
| 13.015 | Blindenergie | kVARh |
| 13.100 | Zeitversatz | s |

### DPT 14 — 4-Byte IEEE Float (Auswahl)

Nur eine Teilmenge der 80 DPT-14-Subtypen ist im Sende-UI verfügbar. Alle Subtypen werden im Monitor dekodiert.

| Subtyp | Beschreibung | Einheit |
|---------|-------------|--------|
| 14.007 | Winkel | ° |
| 14.019 | Strom | A |
| 14.027 | Spannung | V |
| 14.033 | Frequenz | Hz |
| 14.056 | Leistung | W |
| 14.065 | Geschwindigkeit | m/s |
| 14.068 | Temperatur | °C |
| 14.069 | Absolute Temperatur | K |
| 14.070 | Temperaturdifferenz | K |

### DPT 16 — 14-Zeichen-String

| Subtyp | Beschreibung |
|---------|-------------|
| 16.000 | ASCII |
| 16.001 | ISO 8859-1 |

### DPT 20 — 1-Byte Enum

| Subtyp | Beschreibung |
|---------|-------------|
| 20.002 | Gebäudemodus |
| 20.003 | Belegt-Modus |
| 20.004 | Priorität |
| 20.005 | Licht-Anwendungsmodus |
| 20.006 | Licht-Anwendungsbereich |
| 20.007 | Alarmklassentyp |
| 20.008 | PSU-Modus |
| 20.013 | Zeitverzögerung |
| 20.014 | Windstärke (Beaufort) |
| 20.100 | Brennstofftyp |
| 20.101 | Brennertyp |
| 20.102 | HVAC-Modus |
| 20.103 | DHW-Modus |
| 20.104 | Lastpriorität |
| 20.105 | HVAC-Regelmodus |
| 20.106 | HVAC-Notbetrieb |
| 20.107 | Umschaltmodus |
| 20.108 | Ventilmodus |
| 20.109 | Klappenmodus |
| 20.110 | Heizmodus |
| 20.111 | Lüftermodus |
| 20.112 | Master-/Slave-Modus |
| 20.113 | Raum-Sollwert-Status |

> **Hinweis:** Viele DPT-20-Enums werden nur als Rohwert angezeigt. Lesbare Labels (z. B. „Comfort“, „Standby“) sind u. a. für 20.102 (HVAC-Modus) verfügbar.

### DPT 21 — 8-Bit Status Flags

| Subtyp | Beschreibung |
|---------|-------------|
| 21.001 | Allgemeiner Status |
| 21.002 | Geräte-Steuerung |
| 21.100 | Zwangssignal |
| 21.102 | Status Raumheizungsregler |
| 21.103 | Status Solar-DHW-Regler |
| 21.105 | Status Raumkühlungsregler |
| 21.106 | Status Lüftungsregler |

### DPT 22 — 16-Bit Status Flags

| Subtyp | Beschreibung |
|---------|-------------|
| 22.100 | DHW-Reglerstatus |
| 22.101 | RHCC-Status |

### DPT 29 — 8-Byte Signed (64-bit Energie)

| Subtyp | Beschreibung | Einheit |
|---------|-------------|--------|
| 29.010 | Wirkenergie | Wh |
| 29.011 | Scheinenergie | VAh |
| 29.012 | Blindenergie | VARh |

### DPT 232 / 242 / 249 / 250 / 251 / 252 / 254 — Farbe & Licht

| DPT | Beschreibung | Größe |
|-----|-------------|------|
| 232.600 | RGB-Farbe | 3 Byte |
| 242.600 | CIE xyY Farbe | 6 Byte |
| 249.600 | Helligkeit & Farbtemperatur Transition | 6 Byte |
| 250.600 | Helligkeit & Farbtemperatur Control (relativ) | 3 Byte |
| 251.600 | RGBW Farbe | 6 Byte |
| 252.600 | Relative Steuerung RGBW | 5 Byte |
| 254.600 | Relative Steuerung RGB | 3 Byte |

---

## Nur Dekodierung (kein Senden)

Die folgenden DPTs werden im Monitor dekodiert, sofern das ETS-Projekt eine Zuordnung liefert, sind aber nicht im Sende-UI auswählbar.

| DPT | Beschreibung |
|-----|-------------|
| 15.000 | Entrance Access (Zugangscode) |
| 23.x | 2-Bit Action Set (on/off, up/down, alarm) |
| 24.x | Variabler String (ISO 8859-1) |
| 25.x | Double Nibble |
| 26.001 | Scene Info |
| 27.001 | Bit-kombinierte Info Ein/Aus |
| 30.1010 | Channel Activation (24 Kanäle) |
| 206.x | Zeitverzögerung + HVAC/DHW/Belegung/Gebäudemodus |
| 217.001 | DPT-Version |
| 219.001 | Alarm Info |
| 222.x | Raumtemperatur-Sollwerte (×3) |
| 225.x | Scaling Step Time |
| 229.001 | Metering Value |
| 234.001 | Sprachcode (ISO 639-1) |
| 235.001 | Tariff Active Energy |
| 240.800 | Combined Position (Jalousien/Rollläden) |
| 241.800 | Shutter Actuator Status |
| 243.x | xyY Farb-Transition |
| 253.x | Relative Control xyY |
| 275.x | Vier 2-Byte Floats |
