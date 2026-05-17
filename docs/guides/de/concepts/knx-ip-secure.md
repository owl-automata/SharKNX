# KNX IP Secure

KNX IP Secure ist die Sicherheitserweiterung für das KNXnet/IP-Protokoll auf der Transportebene. Es verschlüsselt die Kommunikation zwischen einem KNX-IP-Gerät (Gateway oder Router) und einem Client wie SharKNX. Dadurch wird das Abhören und die unbefugte Steuerung über das IP-Netzwerk effektiv verhindert.

> Diese Seite erklärt, was KNX IP Secure ist und wie SharKNX damit umgeht. Die schrittweise Anleitung zur Einrichtung finden Sie unter [KNX IP Secure einrichten](../how-to/setup-knx-ip-secure.md).

---

## Was KNX IP Secure schützt

In einer Standard-KNXnet/IP-Installation erfolgt der Tunneling-Datenverkehr zwischen einem Client und einem Gateway unverschlüsselt über UDP-Pakete. Jeder, der Zugriff auf dieses Netzwerk hat, kann Telegramme mitschreiben oder beliebige Befehle einspeisen. KNX IP Secure löst dieses Problem, indem es den Tunneling-Transport auf **TCP** umstellt und eine AES-128-CCM-Verschlüsselung auf die Sitzung anwendet. Dies stellt Folgendes sicher:

- Nur Clients mit den korrekten Zugangsdaten können eine Verbindung aufbauen.
- Der Datenverkehr kann von anderen Parteien im Netzwerk weder mitgelesen noch manipuliert (Replay-Angriffe) werden.
- Das Gateway kann Verbindungsversuche von unbekannten Quellen abweisen.

KNX IP Secure arbeitet auf der IP-Transportebene. Es verändert nicht den Inhalt des eigentlichen KNX-Telegramms – das ist die Aufgabe von [KNX Data Secure](knx-data-secure.md).

---

## Die zwei Modi von KNX IP Secure

### Secure Tunneling (Sicheres Tunneling)

Secure Tunneling stellt eine verschlüsselte **TCP**-Verbindung zwischen SharKNX und einer KNX-IP-Secure-fähigen Schnittstelle (in der Regel ein KNX-IP-Gateway oder die Tunneling-Schnittstelle eines KNX-IP-Routers) her. Dies ersetzt den unverschlüsselten UDP-Transport des Standard-KNXnet/IP-Tunnelings. Jede Tunneling-Verbindung besitzt eine eigene Physikalische Adresse der Schnittstelle und entsprechende Zugangsdaten im Schlüsselbund (Keyring).

**Einschränkung der Absenderadresse:** Wenn Sie über einen KNX-IP-Secure-Tunnel verbunden sind, ist die Physikalische Adresse für ausgehende Telegramme fest auf die von der Schnittstelle des Gateways zugewiesene Adresse fixiert. SharKNX kann diese nicht überschreiben. Dies ist besonders wichtig bei der Arbeit mit KNX Data Secure-Gruppenadressen, da diese die Physikalische Adresse des Absenders validieren – Details dazu finden Sie unter [KNX Data Secure](knx-data-secure.md).

### Secure Multicast (IP Routing Secure)

KNX-IP-Router, die IP Routing Secure unterstützen, verwenden einen gemeinsam genutzten symmetrischen Schlüssel – den **Backbone-Schlüssel (Backbone Key)** –, um den Multicast-Verkehr auf der Multicast-Gruppe `224.0.23.12` über **UDP** zu verschlüsseln. Alle Teilnehmer auf der IP-Hauptlinie (Backbone) müssen denselben Schlüssel verwenden.

SharKNX unterstützt Secure Multicast. Wenn ein KNX-IP-Router im Netzwerk gefunden wird, zeigt der **Discovery**-Tab sowohl eine Standard-Multicast-Option als auch eine Secure-Multicast-Option an. Für die Auswahl der Secure-Multicast-Option muss der Backbone-Schlüssel geladen sein.

---

## Dateien für Zugangsdaten (Credential Files)

KNX IP Secure-Zugangsdaten werden über die ETS als Teil des Projekt-Schlüsselbunds exportiert. SharKNX akzeptiert diese Daten in drei Formen:

| Format | Inhalt | Hinweise |
|---|---|---|
| `.knxkeys` | Schnittstellen-Zugangsdaten, Backbone-Schlüssel, Tool-Schlüssel | Verschlüsselt mit einem in der ETS festgelegten projektspezifischen Passwort |
| `.knxproj` | Vollständiges ETS-Projekt inklusive eingebettetem Schlüsselbund | SharKNX extrahiert die benötigten Zugangsdaten automatisch |
| Manuell | Einzelner symmetrischer Backbone-Schlüssel (Eingabe als Hex) | Nur für Secure Multicast; nützlich, wenn Sie nur den Schlüssel und nicht die komplette Schlüsselbund-Datei vorliegen haben |

**Export der `.knxkeys`-Datei aus der ETS:** Öffnen Sie Ihr Projekt in der ETS. Gehen Sie in der Projektübersicht (außerhalb des Projekteditors) auf **Mehr Details → Sicherheit** und wählen Sie **Schlüsselbund sichern**. Vergeben Sie ein Passwort und speichern Sie die Datei.

> **Passwort-Validierung:** SharKNX kann beim Importieren nicht überprüfen, ob ein `.knxkeys`-Passwort korrekt ist – dies liegt an den Spezifikationen des KNX-Standards. Das Passwort wird erst beim tatsächlichen Verbindungsversuch validiert. Wenn die Verbindung mit einem Authentifizierungsfehler fehlschlägt, prüfen Sie, ob das eingegebene Passwort mit dem beim ETS-Export vergebenen Passwort übereinstimmt.

---

## Wo Zugangsdaten in SharKNX geladen werden

Die Zugangsdaten können an drei Stellen in der App hinterlegt werden:

**Sicherheit-Tab (Discovery-Seite):** Der dedizierte Bereich zur Verwaltung aller Sicherheitszertifikate. Tippen Sie auf den Schild-FAB (schwebender Button), um das Importfenster zu öffnen. Nach dem Laden zeigt der Tab eine Übersicht der importierten Daten: wie viele Schnittstellen gefunden wurden und wie viele KNX Data Secure-Geräte in der Datei enthalten waren. Über einen Verlauf-Button können Sie kürzlich verwendete Dateien schnell erneut laden.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-ip-secure/knx-ip-secure-security-tab.png" width="320" alt="Sicherheit-Tab mit einer geladenen Schlüsseldatei sowie der Anzahl an Schnittstellen und Geräten" />
</div>

**Gateway-Karte (Discovery-Tab):** Wenn ein gefundenes Gateway KNX IP Secure unterstützt, enthält dessen Detailblatt den Button **Zugangsdaten laden**. Hier geladene Zugangsdaten werden exakt wie über den Sicherheit-Tab dauerhaft gespeichert.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-ip-secure/knx-ip-secure-gateway-card.png" width="320" alt="Gateway-Detailmenü am unteren Bildschirmrand mit dem Button 'Zugangsdaten laden' für ein KNX IP Secure Gateway" />
</div>

**Optionen-Menü (Zahnrad/Tuning-Symbol) der Discovery-Seite:** Das Tuning-Symbol in der oberen Leiste der Discovery-Seite bietet einen schnellen Zugriff, um Zugangsdaten direkt aus einer `.knxkeys`- oder `.knxproj`-Datei zu laden, ohne den Sicherheit-Tab separat öffnen zu müssen.

Alle Zugangsdaten werden dauerhaft auf dem Gerät gespeichert und bleiben auch nach einem App-Neustart erhalten. Das Laden einer neuen Datei ersetzt die zuvor gespeicherten Daten.

---

## KNX Data Secure Tool-Schlüssel (Tool Keys)

Wenn eine `.knxkeys`-Datei Tool-Schlüssel für KNX Data Secure-Geräte enthält, speichert SharKNX diese Schlüssel automatisch mit ab. Dies ermöglicht verschlüsselte Geräteverwaltungs-Operationen – wie das Umschalten des Programmiermodus, das Auslesen von Geräteinfos, das Zurücksetzen eines Geräts oder das Auslesen von Kommunikationstabellen – bei Geräten, die eine Authentifizierung auf Tool-Ebene erfordern. Diese Schlüssel sind unabhängig von den IP Secure-Tunnel-Zugangsdaten und werden für die Kommunikation auf Geräteebene über KNX TP (Medium) verwendet.

---

## KNX IP Secure vs. KNX Data Secure

| Merkmal | KNX IP Secure | KNX Data Secure |
|---|---|---|
| **Ebene** | IP-Transportebene | KNX-Telegramm (Anwendungsebene) |
| **Was wird verschlüsselt?** | Der UDP-Tunnel oder der Multicast-Kanal | Einzelne Gruppentelegramme auf dem KNX-Medium (TP/RF) |
| **Art der Zugangsdaten** | Schnittstellen-Zertifikat, Backbone-Schlüssel | Gruppen-Schlüssel pro Gruppenadresse |
| **Wo konfigurieren?** | Discovery-Seite $\rightarrow$ Sicherheit-Tab | Projektseite (wird mit der `.knxproj` geladen) |
| **Erforderlich für...** | Verbindung zu einem sicheren IP-Gateway | Senden/Empfangen von sicheren Gruppentelegrammen |

Beide Sicherheitsmechanismen sind vollkommen unabhängig voneinander. Eine KNX-Installation kann KNX IP Secure für die IP-Verbindung nutzen, ohne KNX Data Secure auf dem Bus zu verwenden – oder umgekehrt, oder beide kombiniert.

Weitere Informationen zur Verschlüsselung auf Telegrammebene finden Sie unter [KNX Data Secure](knx-data-secure.md).
