# Verbindung zu einem KNX-Gateway herstellen

SharKNX verbindet sich mit Ihrer KNX-Installation über ein KNXnet/IP-Gateway im lokalen Netzwerk. Diese Anleitung beschreibt, wie Sie ein Gateway automatisch finden, es für die schnelle Wiederverwendung speichern, ein Gateway manuell hinzufügen und die Verbindung herstellen.

---

## Option A — Suchen und Verbinden (Empfohlen für die erste Nutzung)

1. Wechseln Sie auf die **Discovery**-Seite und öffnen Sie den Reiter **Discover**.
2. Tippen Sie auf den **Scan-FAB** (Radar-Symbol). Die App sendet KNXnet/IP-Suchanfragen (Discovery Requests) in das lokale Netzwerk und listet alle antwortenden Gateways auf.
3. Suchen Sie Ihr Gateway in den Ergebnissen. Jede Karte zeigt den Gateway-Namen, die IP-Adresse, den Port und an, ob KNX IP Secure unterstützt wird.
4. Tippen Sie auf **Auswählen** auf der Gateway-Karte, um es als aktives Gateway für die aktuelle Sitzung festzulegen.
   - Um es für zukünftige Sitzungen zu speichern, tippen Sie auf der Karte auf **Speichern**. Gespeicherte Gateways erscheinen im Reiter **Konfig** und können dort direkt ohne erneuten Suchlauf ausgewählt werden.
5. Navigieren Sie zur **Monitor**-Seite (oder einer anderen Seite, die eine Verbindung benötigt) und tippen Sie auf den **Verbinden/Start-FAB**. SharKNX verbindet sich automatisch mit dem ausgewählten Gateway.

> **Zuletzt ausgewähltes Gateway:** Das am häufigsten oder zuletzt verwendete Gateway wird gespeichert und ganz oben im Verbindungs-Pop-up auf den Monitor- und Shark-Hunt-Seiten angezeigt. Das bedeutet, dass Sie die Discovery-Seite nach der Ersteinrichtung normalerweise nicht mehr aufrufen müssen.

---

## Option B — Ein Gateway manuell hinzufügen

Nutzen Sie diese Option, wenn sich das Gateway in einem anderen Subnetz befindet oder nicht über Multicast auffindbar ist (z. B. bei einem Fernzugriff über VPN).

1. Wechseln Sie auf die **Discovery**-Seite und öffnen Sie den Reiter **Konfig**.
2. Tippen Sie auf den **+ FAB**, um das Formular für die manuelle Gateway-Eingabe zu öffnen.
3. Füllen Sie die erforderlichen Felder aus:

   | Feld | Beschreibung |
   |---|---|
   | **Name** | Eine Bezeichnung, um dieses Gateway in der Liste zu identifizieren |
   | **IP-Adresse** | Die IPv4-Adresse des Gateways |
   | **Port** | Der Standardport ist `3671` |
   | **KNX IP Secure verwenden** | Aktivieren Sie dies, wenn das Gateway einen verschlüsselten Secure-Tunnel erfordert |
   | **NAT-Modus** | Aktivieren Sie dies, wenn die Verbindung über einen NAT-Router oder eine Firewall erfolgt |

4. Tippen Sie auf **Speichern**. Das Gateway erscheint in der Liste des Konfig-Tabs und steht sofort zur Auswahl bereit.
5. Tippen Sie auf den Gateway-Eintrag, um es auszuwählen, und starten Sie anschließend den Monitor oder verbinden Sie sich von einer Hunt-Seite aus.

> Der Konfig-Tab unterstützt bis zu **50** gespeicherte Gateways.

---

## Option C — Verbindung über Multicast (KNX IP Routing)

Wenn Ihre Installation einen KNX-IP-Router im Routing-Modus verwendet, kann SharKNX Telegramme direkt über die Multicast-Gruppe empfangen und senden, anstatt sich über einen spezifischen Tunnel mit einem einzelnen Gateway zu verbinden.

1. Wechseln Sie auf die **Discovery**-Seite $\rightarrow$ Reiter **Discover**.
2. Wenn bei einem Suchlauf kein Router mit Routing-Funktionalität gefunden wird, wird der Multicast-Bereich standardmäßig eventuell ausgeblendet. Aktivieren Sie **Multicast-Optionen immer anzeigen** unter **Einstellungen $\rightarrow$ Discover**, um diesen Bereich dauerhaft sichtbar zu machen.
3. Tippen Sie bei der Multicast-Option auf **Auswählen**. Es ist keine Konfiguration von IP-Adresse oder Port erforderlich – die App nutzt die unter Einstellungen $\rightarrow$ Discover hinterlegte Multicast-Adresse und den entsprechenden Port (Standard: `224.0.23.12`, Port `3671`).

---

## Verbinden mit KNX IP Secure

Wenn das Gateway KNX IP Secure erfordert, laden Sie Ihre Zugangsdaten im Reiter **Sicherheit** auf der Discovery-Seite, bevor Sie die Verbindung herstellen. Siehe hierzu [KNX IP Secure einrichten](setup-knx-ip-secure.md).

---

## Fehlerbehebung (Troubleshooting)

| Symptom | Mögliche Ursache |
|---|---|
| Keine Gateways nach dem Scan gefunden | Das Mobilgerät und das Gateway befinden sich in unterschiedlichen Subnetzen oder Multicast wird blockiert – versuchen Sie **Unicast-Subnetz-Scan erzwingen** unter Einstellungen $\rightarrow$ Discover oder fügen Sie das Gateway manuell hinzu. |
| Verbindung läuft in ein Timeout | Die Gateway-IP oder der Port ist falsch, oder das Gateway ist durch einen anderen Client belegt (die meisten Gateways unterstützen nur eine einzige Tunnelverbindung gleichzeitig). |
| Sichere Verbindung schlägt fehl | Die Zugangsdaten wurden nicht geladen oder das Passwort des Schlüsselbunds ist falsch – prüfen Sie den Reiter Sicherheit. |
| Gateway gefunden, kann aber nicht ausgewählt werden | Das Gateway erfordert wahrscheinlich KNX IP Secure und die entsprechenden Zugangsdaten wurden noch nicht in der App geladen. |
