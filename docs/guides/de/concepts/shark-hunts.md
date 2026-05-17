# Shark Hunts (Wiederverwendbare Testabläufe)

Ein **Shark Hunt** ist ein wiederverwendbares, in sich geschlossenes Set von Aktionen zum Testen und Diagnostizieren einer KNX-Installation. Anstatt bei jedem Test mühsam zu einer Gruppenadresse zu navigieren, den Datenpunkttyp auszuwählen und den Befehl neu zu erstellen, konfigurieren Sie einen "Hunt" einmalig. Danach führen Sie ihn mit nur einem Fingertipp aus – von überall und bei jedem zukünftigen Kundeneinsatz auf der Anlage.

---

## Die Kernidee

Jeder Shark Hunt wird als JSON-Datei gespeichert, die eine Sammlung von **Sende-Aktionen** (Befehle an den Bus) und **Monitor-Aktionen** (gefilterte Monitor-Sitzungen) beschreibt. Ein Hunt kann entweder nur einen Typ oder beide kombiniert enthalten. Wenn Sie einen Hunt öffnen, werden alle darin enthaltenen Aktionen als übersichtliche Seite mit antippbaren Karten dargestellt – sofort einsatzbereit.

Das macht Shark Hunts in vielen Praxis-Szenarien äußerst nützlich:

- **Wiederholte Tests bei der Inbetriebnahme.** Die Inbetriebnahme erfordert oft das Dutzendfache Senden derselben Befehle über mehrere Baustellenbesuche hinweg. Ein Hunt speichert diese Befehle, sodass Sie sie nie wieder manuell zusammenstellen müssen.
- **Diagnose delegieren.** Ein Hunt kann alle Verbindungsdetails einer bestimmten KNX-Installation enthalten. Sie können ihn exportieren und mit einem Kollegen oder dem Kunden teilen. Dieser kann den Test auf dem eigenen Gerät ausführen, ohne zu wissen, wie man ein Gateway konfiguriert oder die passenden Gruppenadressen sucht.
- **Strukturierte Testsequenzen.** Eine Mehrfach-/Sequenz-Aktion kann eine Reihe von Befehlen mit konfigurierbaren Verzögerungen (Delays) nacheinander senden. So testen Sie eine komplette Lichtszene oder eine Jalousiefahrt mit nur einem Fingertipp.
- **Erweiterte Bus-Filterung.** Monitor-Aktionen können komplexe Filterlogiken anwenden – einschließlich der Kombination von Gruppenadressbereichen, Gerätefiltern, Telegrammtypen und Zeitfenstern –, die die standardmäßige Filterleiste des Bus-Monitors nicht unterstützt.

---

## Sende-Aktionen (Send Actions)

Es stehen drei Arten von Sende-Aktionen zur Verfügung:

**Fixer Befehl (Send Fixed)** führt jedes Mal einen einzelnen Schreib- oder Lesebefehl (*Write* / *Read*) an eine bestimmte Gruppenadresse mit einem fest hinterlegten Wert aus. Ideal für schnelle Gerätetests – z. B. Licht einschalten, Szene speichern oder einen Sensorwert abfragen.

**Mehrfachbefehl / Sequenz (Send Multiple / Sequence)** führt eine Reihe von fixen Befehlen nacheinander aus. Jeder Befehl in der Sequenz kann eine konfigurierbare Verzögerung besitzen, bevor der nächste ausgelöst wird (bis zu 10 Sekunden pro Schritt). Perfekt zum Testen von Lichtszenen, Jalousie-Laufzeiten oder mehrstufigen Logiken.

**Variabler Befehl (Send Variable)** sendet einen Wert, den Sie erst im Moment der Ausführung flexibel auswählen, an eine oder mehrere Gruppenadressen mit demselben Datenpunkttyp (DPT). Wenn Sie die Aktionskarte antippen, öffnet sich ein Eingabefenster mit den passenden DPT-Steuerelementen (Slider, Dimmer, Farbwähler, numerische Felder etc.). Ideal für maximale Flexibilität, ohne den Hunt bearbeiten zu müssen.

---

## Monitor-Aktionen (Monitor Actions)

Es stehen drei Arten von Monitor-Aktionen zur Verfügung:

**Benutzerdefinierter Monitor (Custom Monitor)** wendet einen Filter mit mehreren Bedingungen auf den Bus-Monitor an. Bedingungen können nach Gruppenadresse (inklusive Wildcards wie `1/*/0`), nach der physikalischen Quelladresse des Senders (inklusive Wildcards wie `1.*.*`), nach Telegrammtyp (Lesen, Schreiben, Antwort), nach Name/Beschreibungstext oder nach Zeitfenster filtern. Die Bedingungen werden über UND/ODER-Logiken verknüpft. Dies ermöglicht komplexe Filter, die über die normale Monitor-Suchleiste nicht realisierbar sind. Adress- und Geräteeinträge können zudem auf "Ausschließen" statt "Einschließen" gesetzt werden, um beispielsweise alles außer einer bestimmten Linie zu überwachen.

**Raum-Monitor (Monitor Space)** nutzt die Gebäudestruktur Ihres ETS-Projekts als Filterziel. Sie wählen einfach einen Raum oder Bereich aus der Gebäudehierarchie, und der Monitor zeigt nur noch die Gruppenadressen oder Geräte an, die diesem Raum zugeordnet sind. Keine manuelle Adresseingabe erforderlich.

**Geräte-Monitor (Monitor Device)** nimmt gezielt ein oder mehrere bestimmte Geräte aus Ihrem ETS-Projekt ins Visier und überwacht alle mit ihnen verknüpften Gruppenadressen. Äußerst effektiv, um die Buskommunikation eines einzelnen Aktors oder Sensors während der Diagnose zu isolieren.

Sobald Sie eine Monitor-Aktion in einem Hunt öffnen, werden die Filter sofort aktiv. Ein Badge in der Monitor-Ansicht zeigt die Details des aktiven Filters an, und über ein Schnellwechsel-Menü können Sie direkt zwischen allen Monitor-Aktionen des Hunts hin- und herwechseln, ohne die Monitor-Seite zu verlassen.

---

## Teilen und Portabilität

Shark Hunts sind auf maximale Portabilität ausgelegt. Jeder Hunt kann optional ein **vorkonfiguriertes IP-Gateway** beinhalten – inklusive IP-Adresse, Port und Verbindungseinstellungen der Anlage, für die er erstellt wurde. Wenn jemand einen geteilten Hunt öffnet, erscheint dieses Gateway direkt als Verbindungsoption. Der Empfänger kann sich sofort verbinden und den Hunt ausführen, ohne selbst einen Suchlauf (Discovery) oder eine Konfiguration durchführen zu müssen.

Sie können einen einzelnen Hunt oder alle Ihre Hunts gesammelt als JSON-Datei exportieren und über beliebige Wege teilen – per Messenger, E-Mail oder Cloud-Speicher. Das Importieren einer JSON-Datei fügt die enthaltenen Hunts nahtlos Ihrer Liste hinzu, ohne bestehende Einträge zu überschreiben.

Die Hunt-Karten sind farblich gekennzeichnet, sodass Sie auf einen Blick sehen, was ein Hunt beinhaltet:

| Rahmenfarbe | Inhalt |
|---|---|
| Grün | Nur Sende-Aktionen |
| Blau | Nur Monitor-Aktionen |
| Rot | Sowohl Sende- als auch Monitor-Aktionen |

---

## Datenspeicherung (Persistence)

Hunts werden direkt auf Ihrem Gerät gespeichert und bleiben auch nach einem Neustart der App vollständig erhalten. Der Erstellungszeitpunkt sowie der Zeitstempel der letzten Änderung werden für jeden Hunt im Info-Bereich hinterlegt und angezeigt.

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/concepts/shark-hunts/shark-hunts-main-page.png" width="320" alt="Shark Hunts Hauptseite mit Hunt-Karten und farblich gekennzeichneten Rahmen" /></td>
      <td><img src="../../../../assets/screenshots/guides/concepts/shark-hunts/shark-hunts-hunt-page.png" width="320" alt="Eine geöffnete Shark Hunt Seite mit Karten für Sende-Aktionen und Monitor-Aktionen" /></td>
    </tr>
  </table>
</div>

---

## Weiterführende Links

- [Einen Shark Hunt erstellen](../how-to/create-shark-hunt.md) — Schritt-für-Schritt-Anleitung zur Erstellung Ihres ersten eigenen Hunts.
