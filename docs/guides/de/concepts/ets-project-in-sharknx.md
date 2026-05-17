# ETS-Projekte in SharKNX

SharKNX kann Standard-ETS-Projektdateien (`.knxproj`) laden, um jeden Bereich der App mit den Klarnamen, Datenpunkttypen (DPT) und Strukturen anzureichern, die Sie bereits in der ETS definiert haben. Diese Seite erklärt, was das in der Praxis bedeutet – was SharKNX mit der Datei macht, was die App bewusst *nicht* tut und was Sie beachten sollten.

---

## Die Projektdatei wird niemals verändert

Das Laden einer `.knxproj`-Datei in SharKNX ist ein reiner Lesevorgang (Read-Only). SharKNX liest die Datei einmalig aus, extrahiert die benötigten Daten und speichert sie intern in der App ab. **Die Originaldatei auf Ihrem Gerät wird zu keinem Zeitpunkt überschrieben oder verändert.** Sie müssen sich also keine Sorgen machen, dass SharKNX Ihr Projekt beschädigt, Versionskonflikte verursacht oder Probleme erzeugt, wenn Sie dasselbe Projekt später wieder in der ETS öffnen.

---

## Was das Laden eines Projekts freischaltet

Ohne Projekt funktioniert SharKNX ebenfalls – Sie können sich mit einem Gateway verbinden, den Bus überwachen und Befehle über die reine Eingabe von Gruppenadressen senden. Alles ist funktionsfähig, aber eben ohne Namen. Das Laden eines Projekts hebt die Bedienung auf ein völlig neues Level:

**Projektseite — Vier strukturierte Ansichten:**
Die Reiter Gruppenadressen, Geräte, Topologie und Gebäude werden vollständig mit den Daten aus Ihrem Projekt befüllt und spiegeln exakt die Struktur wider, die Sie aus der ETS kennen. Sie können die gesamte Hierarchie durchsuchen, nach Namen filtern und jede Gruppenadresse direkt antippen, um sofort einen Lese- (Read) oder Schreibbefehl (Write) abzusetzen.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/ets-project-in-sharknx/ets-project-group-addresses.png" width="320" alt="Projektseite mit dem Gruppenadressen-Baum einschließlich Hauptgruppen, Mittelgruppen und Gruppenadressen aus einem geladenen ETS-Projekt" />
</div>

**Monitor-Seite — Benannte und dekodierte Telegramme:**
Eintreffende Telegramme werden automatisch mit dem geladenen Projekt abgeglichen. Jede Zeile im Monitor zeigt direkt den Namen der Gruppenadresse sowie einen menschenlesbaren, dekodierten Wert basierend auf seinem Datenpunkttyp an – anstelle von unverständlichen Hexadezimalwerten. Auch der Befehls-Editor nutzt das Projekt, um den Namen der Gruppenadresse und den DPT automatisch vorauszufüllen, wenn Sie eine Gruppenadresse auswählen.

**KNX Data Secure — Automatische Schlüsselextraktion:**
Wenn Ihr Projekt Data Secure-Gruppenadressen enthält, werden deren Gruppenschlüssel vollautomatisch extrahiert. SharKNX nutzt diese, um eingehende verschlüsselte Telegramme im Monitor direkt lesbar zu machen und ausgehende Data Secure-Befehle zu verschlüsseln. Für die Sicherheit auf Gruppenebene ist kein separater Import von Zertifikaten erforderlich. Details dazu finden Sie unter [KNX Data Secure](knx-data-secure.md).

---

## Kommunikationsobjekte

Wenn die Option **Kommunikationsobjekte laden** (standardmäßig aktiv) eingeschaltet ist, analysiert und speichert SharKNX auch die Kommunikationsobjekte für jedes Gerät, mit dem Gruppenadressen verknüpft sind. Dies sorgt für eine enorme Detailtiefe:

- Im Reiter "Geräte" können Sie für jedes Gerät eine dedizierte Kommunikationsobjekte-Seite öffnen. Diese zeigt alle verknüpften Kommunikationsobjekte inklusive ihrer Flags (K-L-S-Ü-A), Größen, Funktionen und verbundenen Gruppenadressen.
- Dies ist besonders nützlich für die Fehldiagnose an Geräten: Sie sehen auf einen Blick, welches Kommunikationsobjekt auf welche Gruppenadresse hört, und können Testbefehle direkt aus dieser Ansicht heraus senden.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/ets-project-in-sharknx/ets-project-comm-objects.png" width="320" alt="Seite mit Kommunikationsobjekten für ein Gerät, die Objektnummer, Flags, Funktion, Größe und verknüpfte Gruppenadressen anzeigt" />
</div>

Das Deaktivieren dieser Option reduziert den Speicherbedarf der App, was vor allem auf älteren Mobilgeräten mit begrenztem Arbeitsspeicher (RAM) oder bei extrem großen Projekten sinnvoll sein kann. Die restlichen Projektdaten (Gruppenadressen, Topologie, Gebäude) werden dennoch ganz normal geladen.

---

## Was SharKNX NICHT tut

SharKNX ist ein Werkzeug für den Vor-Ort-Einsatz auf der Baustelle oder Anlage (Field Tool) und kein Inbetriebnahme-Werkzeug. Folgende Dinge sind der ETS vorbehalten und werden von SharKNX bewusst nicht unterstützt:

- **Keine Parameteränderungen:** SharKNX kann keine im Projekt gespeicherten Geräteparameter auslesen oder verändern. Das Parametrieren von Geräten bleibt exklusiv der ETS vorbehalten.
- **Kein Download von Applikationsprogrammen:** SharKNX kann keine Geräte mit ihrer Applikationssoftware bespielen oder flashen.
- **Keine Verbindung zum ETS-Server oder einer Lizenz:** SharKNX liest die exportierte `.knxproj`-Datei direkt und lokal aus. Es stellt keine Verbindung zur ETS-Software her, benötigt keine laufende ETS im Hintergrund und verbraucht dementsprechend auch keine ETS-Lizenz.

Das **Programmieren der Physikalischen Adresse** ist die einzige Schreiboperation, die SharKNX im Kontext von Projektdaten unterstützt – allerdings schreibt die App hierbei über KNX-Management-Kommunikation direkt in das physische Gerät auf dem Bus und niemals in die `.knxproj`-Datei. Die Projektdatei selbst bleibt stets unberührt.

---

## Projektdaten aktuell halten

SharKNX liest die Projektdatei exakt in dem Moment aus, in dem Sie diese laden. Wenn Sie anschließend Änderungen in der ETS vornehmen und eine neue `.knxproj`-Datei exportieren, bekommt SharKNX dies nicht automatisch mit – Sie müssen die aktualisierte Datei einfach erneut in die App laden.

Die Funktion **Projektdaten anwenden** im Optionen-Menü (Tuning-Symbol) der Monitor-Seite hilft Ihnen hierbei: Nach dem Laden eines aktualisierten Projekts können Sie die neuen Namen und Datenpunkttypen auf bereits aufgezeichnete Telegramme in der Monitorliste anwenden, ohne die Bus-Aufzeichnung neu starten zu müssen.

---

## Unterstützte Formate

| Format | Unterstützt |
|---|---|
| `.knxproj` (ETS5) | ✅ |
| `.knxproj` (ETS6) | ✅ |
| Passwortgeschützte Projekte | ✅ (Passwortabfrage erfolgt direkt beim Import) |
| `.knxpkg` oder andere ETS-Formate | — |

Es kann immer nur ein Projekt gleichzeitig in der App aktiv sein. Das Laden eines neuen Projekts ersetzt das aktuell geladene. Zuvor verwendete Projekte werden jedoch in einer Verlaufsliste gespeichert, sodass Sie sie schnell wieder aufrufen können, ohne das Dateisystem Ihres Geräts erneut durchsuchen zu müssen.
