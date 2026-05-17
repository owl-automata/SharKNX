# Die Discovery-Seite

Die Discovery-Seite ist die erste Seite in der unteren Navigationsleiste und öffnet sich standardmäßig beim Start der App. Hier können Sie KNX-IP-Gateways suchen, konfigurieren und verwalten, um eine Verbindung zur Anlage herzustellen. Die Seite ist in drei Reiter unterteilt: **Discover**, **Konfig** und **Sicherheit**.

---

## Reiter "Discover"

Tippen Sie auf den **Scan-FAB** (schwebender Button mit Radar-Symbol), um die Suche nach KNX-IP-Geräten im lokalen Netzwerk zu starten. Die App sendet KNX-IP-Suchanfragen (Discovery Requests) und listet alle antwortenden Geräte als Karten auf.

### Gateway-Karten

Jede gefundene Gateway-Karte zeigt Folgendes an:
- Gateway-Name (wie vom Gerät übermittelt)
- IP-Adresse und Tunnel-Port

Auf jeder Karte befinden sich zwei Schaltflächen:

**Auswählen (Select)** — markiert dieses Gateway als aktives Verbindungsziel. Das Gateway wird in den Bereich **Zuletzt ausgewähltes Gateway** ganz oben auf der Seite verschoben und bleibt auch nach einem App-Neustart gespeichert. Das Auswählen eines Gateways stellt nicht sofort eine Verbindung her; die App verbindet sich automatisch, sobald Sie eine Aktion ausführen (z. B. den Monitor starten oder einen Befehl senden).

**Speichern (Save)** — sichert das Gateway im Reiter **Konfig**, sodass es ohne erneuten Suchlauf direkt wiederverwendet werden kann. Das ist besonders praktisch, wenn Sie dieselbe Anlage regelmäßig besuchen.

Ein Tippen auf die Karte selbst (nicht auf eine der Schaltflächen) öffnet das **Gateway-Detailblatt** am unteren Bildschirmrand:
- Physikalische KNX-Adresse
- Seriennummer
- MAC-Adresse
- Medientyp
- Gerätemanagement-Funktionen (sofern unterstützt)
- **Verbinden-Button** — stellt sofort eine Verbindung her; nützlich, um die Erreichbarkeit zu testen, obwohl dies für den normalen Betrieb nicht zwingend erforderlich ist.
- **Zugangsdaten laden-Button** *(nur bei KNX IP Secure-Gateways)* — lädt die passenden `.knxkeys`- oder `.knxproj`-Zugangsdaten für dieses Gateway. Siehe hierzu [KNX IP Secure](../concepts/knx-ip-secure.md).

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/pages/discovery/discovery-scan.png" width="320" alt="Reiter Discover mit gefundenen Gateway-Karten sowie den Schaltflächen Auswählen und Speichern" /></td>
      <td><img src="../../../../assets/screenshots/guides/pages/discovery/discovery-gateway-detail.png" width="320" alt="Gateway-Detailblatt am unteren Bildschirmrand mit Anzeige von Adresse, Seriennummer, MAC und Verbinden-Button" /></td>
    </tr>
  </table>
</div>

### Zuletzt ausgewähltes Gateway

Wenn zuvor bereits ein Gateway ausgewählt wurde, erscheint es in einem oben angehefteten Bereich des Discover-Reiters. Es wird beim App-Neustart automatisch wieder ausgewählt, sodass Sie direkt mit der Arbeit beginnen können, ohne einen neuen Suchlauf zu starten.

### Multicast-Bereich

Wird ein KNX-IP-Router mit Routing-Funktionalität gefunden, erscheint unterhalb der Kartenliste ein **Multicast**-Bereich. Beim Aufklappen werden zwei Optionen angezeigt:
- **Multicast** — Standard-KNX-IP-Multicast über `224.0.23.12:3671`
- **Secure Multicast** — verschlüsseltes Multicast, das einen Backbone-Schlüssel erfordert (siehe [KNX IP Secure](../concepts/knx-ip-secure.md))

Wählen Sie eine der Optionen aus, um diese anstelle eines Unicast-Tunnels als Verbindungstyp zu nutzen.

---

## Reiter "Konfig"

Der Konfig-Reiter speichert alle Gateways, die Sie manuell oder über den **Speichern**-Button im Discover-Tab hinterlegt haben. Die hier aufgelisteten Gateways stehen jederzeit zur Verfügung, ohne dass ein Suchlauf erforderlich ist.

### Ein Gateway manuell hinzufügen

Tippen Sie auf den **"+" FAB**, um die Seite für die manuelle Gateway-Konfiguration zu öffnen. Füllen Sie folgende Felder aus:

| Feld | Beschreibung |
|---|---|
| **Anzeigename** | Eine Bezeichnung auf der Karte, um dieses Gateway in der Liste zu identifizieren. |
| **IP-Adresse / Hostname** | Die IP-Adresse des Gateways oder ein DNS-Hostname (z. B. eine DynDNS-Domain). |
| **Physikalische KNX-Adresse** | Die KNX-Adresse des Gateways; Standardwert ist `15.15.255`. Muss bei KNX IP Secure-Verbindungen exakt mit dem echten Gerät übereinstimmen. |
| **Port** | Der Tunnel-Port; Standardwert ist `3671`. |
| **NAT verwenden** | Aktivieren Sie dies für VPN-Szenarien, bei denen sich das Mobilgerät und das Gateway in unterschiedlichen Subnetzen befinden. |
| **KNX IP Secure** | Kennzeichnet diese Verbindung als verschlüsselte KNX IP Secure-Verbindung. |

Tippen Sie auf **Speichern**, um den Eintrag zu erstellen. Das Gateway erscheint daraufhin als Karte im Konfig-Reiter.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/discovery/discovery-config-manual.png" width="320" alt="Manuelle Gateway-Konfigurationsseite mit Feldern für Name, IP, Port und Secure-Optionen" />
</div>

### Konfig-Gateway-Karten

Die Karten im Konfig-Reiter funktionieren exakt wie die Karten im Discover-Reiter (Auswählen, Speichern, Detailblatt), bieten jedoch eine Erweiterung: Einen **Bearbeiten-Button**, der die Konfigurationsseite erneut öffnet. So können Sie Felder korrigieren oder aktualisieren, ohne den Eintrag komplett löschen und neu anlegen zu müssen.

Der Konfig-Reiter kann maximal 50 gespeicherte Gateways aufnehmen.

---

## Reiter "Sicherheit"

Im Reiter "Sicherheit" laden Sie die KNX IP Secure- und KNX Data Secure-Zugangsdaten, die app-weit angewendet werden sollen.

Tippen Sie auf den **Schild-FAB** (Schild-Symbol), um das Menü für den Import von Zugangsdaten zu öffnen. Drei Importmethoden stehen zur Verfügung:

| Methode | Anwendungsfall |
|---|---|
| **`.knxkeys`-Datei** | Aus der ETS exportiert. Enthält Schnittstellen-Zugangsdaten, den Backbone-Schlüssel und Werkzeugschlüssel (Tool Keys). Erfordert das beim Export vergebene Schlüsselbund-Passwort. |
| **`.knxproj`-Datei** | Vollständiger ETS-Projektexport. SharKNX extrahiert alle Sicherheitszertifikate und Schlüssel automatisch. |
| **Manueller Backbone-Schlüssel** | Geben Sie einen Multicast-Backbone-Schlüssel direkt als Hexadezimalwert ein. Nur für sicheres Multicast (Secure Multicast) erforderlich. |

Nach dem Ladevorgang zeigt der Reiter eine Zusammenfassung an:
- Wie viele KNX-IP-Schnittstellen in der Datei gefunden wurden.
- Wie viele KNX Data Secure-Geräte (aufgeteilt nach Physikalischer Adresse) vorhanden waren.

Über einen **Verlauf-Button** ganz oben können Sie kürzlich verwendete Zugangsdaten-Dateien schnell wieder aufrufen, ohne das Dateisystem Ihres Geräts erneut durchsuchen zu müssen.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/discovery/discovery-security-tab.png" width="320" alt="Reiter Sicherheit mit einer Zusammenfassung der geladenen Zugangsdaten-Datei inklusive der Anzahl an Schnittstellen und Geräten" />
</div>

> **Werkzeugschlüssel (Tool Keys):** Eine `.knxkeys`-Datei kann auch Werkzeugschlüssel für KNX Data Secure-Geräte enthalten. Falls vorhanden, speichert SharKNX diese automatisch, um verschlüsselte Gerätemanagement-Operationen (wie das Umschalten des Programmiermodus, Auslesen von Geräteinfos etc.) zu ermöglichen. Siehe hierzu [KNX Data Secure](../concepts/knx-data-secure.md).

---

## Das Optionen-Menü (Tuning-Symbol)

Das Tuning-Symbol in der oberen Statusleiste öffnet ein schnelles Menü am unteren Bildschirmrand, über das Sie direkt auf den Import von Zugangsdaten zugreifen können, ohne erst zum Reiter "Sicherheit" navigieren zu müssen:

- **Zugangsdaten aus .knxkeys laden** — öffnet die Dateiauswahl für eine `.knxkeys`-Datei.
- **Zugangsdaten aus .knxproj laden** — öffnet die Dateiauswahl für eine `.knxproj`-Datei.
