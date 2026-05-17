# Eine KNX-Buslinie scannen

Ein Linien-Scan prüft jede einzelne Physikalische Adresse auf einer KNX-Linie und listet alle Geräte auf, die antworten. Dadurch können Sie unabhängig von einem ETS-Projekt überprüfen, was tatsächlich auf der Anlage installiert ist – der schnellste Weg, um sich einen Überblick über eine unbekannte Installation zu verschaffen.

---

## Voraussetzungen

- Eine aktive Verbindung zu einem KNX-Gateway (siehe [Verbindung zu einem Gateway herstellen](connect-to-gateway.md)).
- Die KNX-Bereichs- und Liniennummer, die Sie scannen möchten (z. B. Bereich 1, Linie 1 $\rightarrow$ `1.1`).

---

## Vorgehensweise

1. Wechseln Sie auf die Seite **Management** und öffnen Sie den Reiter **Linien-Scan (Line Scan)**.
2. Konfigurieren Sie den Scan in der Karte **Scan-Einstellungen**:

   | Einstellung | Beschreibung |
   |---|---|
   | **Bereich / Linie** | Der zu scannende Bereich und die Linie (z. B. `1.1`). Tippen Sie auf **Aus Projekt wählen**, um eine Linie direkt aus Ihrem geladenen ETS-Projekt zu übernehmen – dies stellt auch den Medientyp automatisch ein. |
   | **Medientyp** | TP (Twin Pair), IP oder IoT. Muss mit dem physischen Medium der Linie übereinstimmen. |
   | **Bereich (Range)** | Start- und Endadresse der Geräte innerhalb der Linie (0–255). Grenzen Sie diesen Bereich ein, um den Scan zu beschleunigen oder nur ein bestimmtes Segment zu prüfen. |

3. Tippen Sie auf den **Scan-FAB**, um den Vorgang zu starten. Der Scan kann jederzeit abgebrochen werden.
4. Gefundene Geräte werden als Karten dargestellt. Die obere Rahmenfarbe signalisiert den Gerätetyp:

   | Farbe | Typ |
   |---|---|
   | Blau | KNX-Koppler (Linien-/Bereichskoppler) |
   | Rot | Standard-Anwendungsgerät / KNX-Teilnehmer |
   | Grün | KNX Secure-Gerät |

---

## Geräte-Info für alle gefundenen Geräte auslesen

Tippen Sie nach Abschluss des Scans auf **Geräte-Info auslesen** (oberhalb der Kartenliste). Die App liest nun nacheinander Hersteller, Seriennummer und weitere Details für jedes gefundene Gerät ein.

Dies ist besonders nützlich für:
- Die schnelle Erstellung einer Bestandsliste einer Anlage, die Sie nicht selbst in Betrieb genommen haben.
- Den Abgleich mit einem ETS-Projekt, um zu prüfen, ob es mit der physischen Installation übereinstimmt.
- Das Aufspüren von Geräten mit unerwarteten Adressen oder falschen Typen.

---

## Mit einzelnen Gerätekarten arbeiten

Tippen Sie auf eine beliebige Karte, um deren Detailblatt zu öffnen. Von dort aus können Sie folgende Aktionen ausführen:

- **Prüfen (Check)** — Validiert, ob das Gerät noch antwortet.
- **Info auslesen (Read Info)** — Ruft vollständige Gerätedetails ab (Hersteller, Firmware, Betriebszustand etc.).
- **Programmiermodus umschalten (Toggle Programming Mode)** — Aktiviert oder deaktiviert den Programmiermodus des Geräts aus der Ferne.
- **Neustart (Restart)** — Sendet einen Reset-Befehl an das Gerät.
- **Adresse programmieren** — Weist dem Gerät eine neue Physikalische Adresse zu (siehe [Die Physikalische Adresse eines Geräts programmieren](program-device-address.md)).
- **Kommunikation rekonstruieren** — Öffnet den Reiter *Inspect* vorausgefüllt mit der Adresse dieses Geräts, um dessen Kommunikationstabellen auszulesen.

---

## Scan-Ergebnisse exportieren

Tippen Sie auf das **Optionen-Menü (Tuning-Symbol)** in der oberen Leiste, um das aktuellste Scan-Ergebnis zu exportieren:
- **Als Text exportieren** — Generiert einen TXT-Bericht mit Zeitstempel des Scans, Gateway, Bereich/Linie, Medium und der Geräteliste.
- **Als PDF exportieren** — Exportiert dieselben Inhalte in einem sauberen PDF-Format.
