# Die Physikalische Adresse eines Geräts programmieren

SharKNX kann eine Physikalische Adresse direkt von Ihrem Smartphone oder PC aus in ein KNX-Gerät programmieren (schreiben) – ganz ohne ETS oder einen Laptop vor Ort an der Anlage zu benötigen. Hierfür stehen zwei Methoden zur Verfügung: über den physischen Programmierknopf am Gerät oder über die Seriennummer des Geräts (kein Knopfdruck erforderlich).

---

## Voraussetzungen

- Eine aktive Verbindung zu einem KNX-Gateway (siehe [Verbindung zu einem Gateway herstellen](connect-to-gateway.md)).
- Die neue Physikalische Adresse, die Sie zuweisen möchten – entweder aus Ihrem Projekt bekannt oder manuell eingegeben.

---

## Methode A — Über den Programmierknopf

Nutzen Sie diese Methode, wenn Sie physischen Zugang zum Gerät haben (oder ein Kollege vor Ort auf der Baustelle den Knopf für Sie drücken kann).

1. Wechseln Sie auf die Seite **Management** und öffnen Sie den Reiter **Linien-Scan (Line Scan)**.
2. Führen Sie einen Linien-Scan im entsprechenden Bereich durch (siehe [Eine Buslinie scannen](scan-bus-line.md)) und tippen Sie anschließend auf die Karte des Geräts, das Sie neu programmieren möchten, um dessen Detailblatt zu öffnen.
   - Alternativ können Sie auf der Seite **Management** den Reiter **Geräte (Devices)** öffnen, die aktuelle Physikalische Adresse des Geräts eingeben und die Aktionen von dort aus starten.
3. Tippen Sie im Detailblatt des Geräts auf **Adresse programmieren**.
4. Geben Sie die neue Physikalische Adresse in das Eingabefeld ein oder tippen Sie auf das **Lupe-Symbol**, um eine freie Adresse aus Ihrem geladenen ETS-Projekt auszuwählen.
5. Tippen Sie auf **Über Programmierknopf programmieren**.
6. Die App wartet nun bis zu **20 Sekunden** lang darauf, dass ein Gerät in den Programmiermodus versetzt wird. Drücken Sie innerhalb dieses Zeitfensters den Programmierknopf am physischen Gerät.
7. Sobald die App ein Gerät im Programmiermodus auf dem Bus erkennt, schreibt sie die neue Adresse und bestätigt den Erfolg.

> Die App prüft vorab automatisch, ob die neue Adresse bereits von einem anderen Gerät auf der realen Anlage verwendet wird. Wird ein Konflikt erkannt, erhalten Sie eine Warnung, bevor der Schreibvorgang endgültig ausgeführt wird.

---

## Methode B — Über die Seriennummer

Nutzen Sie diese Methode, wenn Ihnen die Seriennummer des Geräts bereits aus einer vorherigen **Info auslesen**-Operation bekannt ist. Es ist kein physischer Knopfdruck am Gerät erforderlich – ideal für Geräte an schwer zugänglichen Stellen (z. B. in der Zwischendecke oder in tiefen Unterputzdosen).

1. Stellen Sie zunächst sicher, dass die Seriennummer des Geräts bekannt ist: Führen Sie hierzu **Info auslesen** über die Gerätekarte im Linien-Scan oder im Reiter "Geräte" aus, falls noch nicht geschehen.
2. Tippen Sie im Detailblatt des Geräts oder im Reiter "Geräte" auf **Adresse programmieren**.
3. Geben Sie die neue Physikalische Adresse ein oder wählen Sie diese aus dem Projekt.
4. Tippen Sie auf **Über Seriennummer programmieren**.
5. Die App spricht das Gerät direkt über seine eindeutige Seriennummer an und schreibt die neue Adresse, ohne dass der Programmierknopf gedrückt werden muss.

---

## Profi-Tipp — Programmiermodus aus der Ferne umschalten

Wenn Sie den Programmierknopf physisch nicht erreichen können, nutzen Sie die Funktion **Programmiermodus umschalten (Toggle Programming Mode)** auf der Gerätekarte oder im Reiter "Geräte", um den Programmiermodus des Geräts per Busbefehl aus der Ferne zu aktivieren. Starten Sie direkt im Anschluss den Vorgang **Über Programmierknopf programmieren** – die App erkennt das Gerät sofort innerhalb des 20-Sekunden-Fensters. Schalten Sie den Modus nach erfolgreicher Programmierung auf demselben Weg wieder aus.

---

## Wichtige Hinweise

- Überprüfen Sie das Ergebnis nach der Programmierung, indem Sie auf der Gerätekarte auf **Prüfen (Check)** tippen. Damit bestätigen Sie, dass das Gerät unter der neuen Adresse auf dem Bus erreichbar ist.
- Dieser Workflow unterstützt die klassische Erstinbetriebnahme vor Ort: Linie scannen $\rightarrow$ alle Geräte identifizieren $\rightarrow$ Physikalische Adressen programmieren $\rightarrow$ anschließend in der ETS verbinden und die Applikationsprogramme einspielen.
