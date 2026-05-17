# Einstellungen – Referenz

Die Seite „Einstellungen“ ist von jedem Bildschirm aus erreichbar, indem Sie auf das **Zahnrad-Symbol** (⚙️) oben rechts in der App-Leiste tippen.

Die Seite gruppiert alle konfigurierbaren Optionen in verschiedene Abschnitte. Ein **Suchsymbol** (🔍) in der oberen Leiste ermöglicht es Ihnen, direkt zu einem Abschnitt anhand seines Namens zu springen.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-overview.png" width="320" alt="Einstellungsseite — vollständige Abschnittsliste" />
</div>

---

## Discovery-Einstellungen

Steuert, wie die App KNX-IP-Gateways im Netzwerk sucht und Verbindungen zu ihnen herstellt.

<div align="center">
  <table>
    <tr>
      <td><img src="../../../../assets/screenshots/guides/settings/settings-discover-a.png" width="320" alt="Discovery-Einstellungen (1 von 2)" /></td>
      <td><img src="../../../../assets/screenshots/guides/settings/settings-discover-b.png" width="320" alt="Discovery-Einstellungen (2 von 2)" /></td>
    </tr>
  </table>
</div>

### Multicast

| Einstellung | Standard | Beschreibung |
|---|---|---|
| Multicast-Adresse | `224.0.23.12` | Die IP-Multicast-Gruppenadresse für KNX-IP-Discovery und Routing. Ändern Sie diese nur, wenn Ihr Netzwerk eine nicht standardisierte Multicast-Gruppe verwendet. |
| Multicast-Port | `3671` | Der UDP-Port für Multicast-Discovery- und Routing-Kommunikation. |

### Discovery-Verhalten

| Einstellung | Standard | Beschreibung |
|---|---|---|
| Multicast-Optionen immer anzeigen | Aus | Wenn aktiviert, sind Multicast-Verbindungsoptionen im Discovery-Tab immer sichtbar. Wenn deaktiviert, erscheinen sie nur, wenn bei einem Scan ein KNX-IP-Router mit Routing-Funktion erkannt wird. |
| Unicast-Subnetz-Scan erzwingen | Aus | Wenn aktiviert, sendet die App nach den Multicast-Discovery-Anfragen zusätzlich individuelle Unicast-Suchanfragen an jede IP-Adresse im aktuellen Subnetz. Nützlich in WLAN-Netzwerken, in denen Router Multicast-Pakete verwerfen können. Falls über Multicast kein Gateway gefunden wird, wird unabhängig von dieser Einstellung automatisch ein Unicast-Scan als Fallback ausgeführt. |

### Timeouts

| Einstellung | Standard | Min | Max | Beschreibung |
|---|---|---|---|---|
| Discovery-Timeout | 3 s | 1 s | 10 s | Gibt an, wie lange die App nach dem Senden von Discovery-Anfragen auf Gateway-Antworten wartet. Erhöhen Sie diesen Wert in langsamen oder stark ausgelasteten Netzwerken. |
| Verbindungs-Timeout | 3 s | 1 s | 10 s | Gibt an, wie lange die App beim Aufbau einer Tunnelverbindung zu einem Gateway wartet, bevor dieses als nicht erreichbar behandelt wird. |

---

## Projekteinstellungen

Steuert, wie ETS-Projektdateien analysiert und angezeigt werden.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-project.png" width="320" alt="Projekteinstellungen" />
</div>

| Einstellung | Standard | Beschreibung |
|---|---|---|
| Kommunikationsobjekte laden | Ein | Wenn aktiviert, analysiert und speichert die App Kommunikationsobjekte für jedes Gerät im Projekt, dem mindestens eine Gruppenadresse zugeordnet ist. Das Deaktivieren reduziert den Speicherverbrauch bei großen Projekten, entfernt jedoch die Ansicht „Kommunikationsobjekte“ von der Projektseite. |
| Elemente pro Seite | 50 | Min: 20 · Max: 200 — Anzahl der gleichzeitig angezeigten Elemente beim Erweitern einer Liste in der Projektbaumansicht (z. B. Gruppenadressen innerhalb einer Mittelgruppe). Sobald das Limit erreicht ist, erscheint eine **Mehr laden**-Schaltfläche (Load more). Niedrigere Werte verbessern die Darstellungsgeschwindigkeit bei großen Projekten. |

---

## Monitor-Einstellungen

Steuert das Verhalten des Busmonitors.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-monitor.png" width="320" alt="Monitor-Einstellungen" />
</div>

| Einstellung | Standard | Beschreibung |
|---|---|---|
| Bildschirm eingeschaltet lassen | Ein | Verhindert, dass sich der Bildschirm des Geräts während einer aktiven Monitor-Sitzung ausschaltet. Empfohlen, da die meisten mobilen Betriebssysteme die IP-Verbindung schließen, sobald sich der Bildschirm ausschaltet. Deaktivieren Sie diese Option, um Akku zu sparen. Beachten Sie jedoch, dass das Monitoring stoppt, sobald sich der Bildschirm ausschaltet. Hinweis: Der Monitor wird immer beendet, wenn die App in den Hintergrund wechselt – unabhängig von dieser Einstellung. |
| Telegramm-Puffergröße | 2000 | Min: 50 · Max: 5000 — Maximale Anzahl von Telegrammen, die gleichzeitig in der Monitorliste gespeichert werden. Sobald das Limit erreicht ist, werden die ältesten Telegramme durch neue überschrieben. Erhöhen Sie diesen Wert für einen längeren Verlauf oder reduzieren Sie ihn, um den Speicherverbrauch auf leistungsschwächeren Geräten zu senken. |

---

## Scan-Einstellungen

Steuert den Programmiermodus-Scan auf der Seite **Management** $\rightarrow$ Tab **Prog. Mode**.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-scan.png" width="320" alt="Scan-Einstellungen" />
</div>

| Einstellung | Standard | Min | Max | Beschreibung |
|---|---|---|---|---|
| Scan-Dauer | 10 s | 4 s | 20 s | Gesamtdauer eines Programmiermodus-Scans. Die App lauscht während dieses Zeitraums auf Geräte im Programmiermodus. |
| Scan-Intervall | 2 s | 1 s | 4 s | Gibt an, wie häufig die App während einer Scan-Sitzung Scan-Signale sendet. Ein kürzeres Intervall erhöht die Wahrscheinlichkeit, ein Gerät zu erkennen, das nur kurz in den Programmiermodus wechselt, erzeugt jedoch mehr Netzwerkverkehr. |

---

## Abonnement

Zeigt den Status Ihres aktuellen Abonnements an und bietet Optionen zur Verwaltung Ihres Tarifs.

<div align="center">
  <img src="../../../../assets/screenshots/guides/settings/settings-subscription.png" width="320" alt="Abonnement" />
</div>

| Element | Beschreibung |
|---|---|
| Aktueller Tarif | Zeigt Ihren aktiven Tarif an: **Free** (Testversion), **Monthly**, **Yearly** oder **Lifetime**. |
| Käufe wiederherstellen | Wendet ein zuvor gekauftes Abonnement erneut auf das aktuelle Gerät an. Verwenden Sie dies nach einer Neuinstallation der App oder beim Wechsel des Geräts. |
| Abonnement kündigen | Öffnet die Verwaltungsseite für Abonnements im App Store (iOS/macOS) oder Google Play (Android), wo Sie ein aktives wiederkehrendes Abonnement kündigen können. Nicht relevant für Lifetime-Tarife. |
| Datenschutzrichtlinie | Link zur [Datenschutzrichtlinie](../../privacy/privacy-en.md) der App. |
| Nutzungsbedingungen | Link zu den [Nutzungsbedingungen](../../terms/terms-en.md) der App. |

---

## Sprache

Öffnet eine Liste der unterstützten Oberflächensprachen der App. Die Auswahl einer Sprache wird sofort übernommen, ohne dass die App neu gestartet werden muss.

Verfügbare Sprachen:

- 🇬🇧 Englisch
- 🇩🇪 Deutsch
- 🇫🇷 Französisch
- 🇪🇸 Spanisch
- 🇮🇹 Italienisch

---

## Design

Legt das visuelle Erscheinungsbild der App fest.

| Option | Beschreibung |
|---|---|
| Hell | Verwendet immer das helle Farbschema. |
| Dunkel | Verwendet immer das dunkle Farbschema. |
| System verwenden | Übernimmt die systemweite Hell-/Dunkelmodus-Einstellung des Geräts. |

---

## Feedback senden

| Option | Beschreibung |
|---|---|
| Bewertung abgeben | Öffnet den Store-Eintrag der App, damit Sie eine Bewertung oder Rezension hinterlassen können. |
| Fehler melden | Öffnet eine vorausgefüllte E-Mail an `info@owl-automata.com`, um ein Problem zu melden. |
| Kontakt aufnehmen | Öffnet eine leere E-Mail an `info@owl-automata.com` für allgemeine Anfragen. |

> Für strukturierte Fehlerberichte siehe auch die Anleitung [How to Report an Issue](../../../support/how-to-report-an-issue.md).

---

## Über

Zeigt die aktuelle Versionsnummer der App sowie Copyright-Informationen an.
