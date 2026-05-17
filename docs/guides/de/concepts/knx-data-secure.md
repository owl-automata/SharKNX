# KNX Data Secure

KNX Data Secure ist die Sicherheitserweiterung für den KNX-Standard auf der Anwendungsebene (Application Layer). Es verschlüsselt und authentifiziert einzelne KNX-Telegramme direkt auf dem Busmedium (TP oder RF). Dadurch schützt es die Daten vor Abfangen und Manipulation – vollkommen unabhängig davon, wie sie zum IP-Netzwerk transportiert werden.

> Diese Seite erklärt, was KNX Data Secure ist und wie SharKNX damit umgeht. Die schrittweise Anleitung zur Einrichtung finden Sie unter [KNX Data Secure einrichten](../how-to/setup-knx-data-secure.md).

---

## Was KNX Data Secure schützt

Standard-KNX-Telegramme, die über die Zweidrahtleitung (Twisted Pair) übertragen werden, können von jedem Gerät im selben Bussegment mitgelesen werden. KNX Data Secure löst dieses Problem, indem es die Nutzdaten ausgewählter Gruppentelegramme mit **AES-128 CCM** verschlüsselt – demselben Algorithmus, der auch bei KNX IP Secure zum Einsatz kommt. Jedes verschlüsselte Telegramm enthält zudem einen **Message Authentication Code (MAC)** und eine fortlaufende **Sequenznummer**. Diese Kombination verhindert:

- **Abhören:** Der Telegramminhalt (Payload) kann ohne den passenden Gruppenschlüssel nicht gelesen werden.
- **Manipulation:** Jede Veränderung an den Nutzdaten führt dazu, dass der MAC ungültig wird und das Telegramm verworfen wird.
- **Replay-Angriffe:** Ein aufgezeichnetes Telegramm kann nicht einfach später erneut gesendet werden, da seine Sequenznummer dann außerhalb der gültigen Reihenfolge liegen würde.

KNX Data Secure arbeitet auf der KNX-Anwendungsebene, also direkt im Telegramm selbst. Es ist völlig unabhängig vom Übertragungsweg – ein Data Secure-Telegramm ist auf der verdrillten Busleitung (TP) oder per Funk (RF) genauso geschützt wie in einem KNXnet/IP-Tunnel.

---

## Gruppenschlüssel und die Absenderliste

Jede KNX Data Secure-Gruppenadresse besitzt ihren eigenen **Gruppenschlüssel (Group Key)**. Dieser Schlüssel wird sowohl für die Verschlüsselung der Nutzdaten als auch für die Berechnung des MAC verwendet. Er ist im ETS-Projekt-Schlüsselbund hinterlegt und wird bei der Inbetriebnahme an alle Geräte verteilt, die mit dieser Gruppenadresse verknüpft sind.

Zusätzlich zur Verschlüsselung führen KNX Data Secure-Geräte eine **Liste vertrauenswürdiger Absender (Trusted Sender List)** pro Gruppenadresse. Dies ist eine Liste von Physikalischen Adressen, deren Telegramme das Gerät akzeptiert. Telegramme, die von einer Physikalischen Adresse stammen, die nicht auf dieser Liste steht, werden lautlos verworfen – selbst wenn die Verschlüsselung korrekt ist. Das bedeutet in der Praxis:

- Um Data Secure-Telegramme korrekt zu **empfangen** und zu deklarieren, benötigen Sie den Gruppenschlüssel.
- Um Data Secure-Befehle zu **senden**, die ein Gerät auch tatsächlich ausführt, muss Ihre Physikalische Adresse auf der Absenderliste des Zielgeräts für diese Gruppenadresse stehen.

---

## Empfang von Data Secure-Telegrammen in SharKNX

SharKNX extrahiert alle Data Secure-Gruppenschlüssel automatisch, sobald Sie eine `.knxproj`-Datei laden. Für das reine Monitoring ist keine separate Einrichtung von Zugangsdaten erforderlich. Nach dem Laden des Projekts gilt:

- Eintreffende Data Secure-Telegramme werden im Monitor transparent entschlüsselt und mit ihrem Klarnamen, dem dekodierten Wert und dem Datenpunkttyp (DPT) angezeigt – exakt wie unverschlüsselte Telegramme.
- Wenn kein Projekt geladen ist, erscheinen Data Secure-Telegramme als rohe Hexadezimalwerte ohne dekodierten Wert (die Nutzdaten sind verschlüsselt und ohne Schlüssel unlesbar).

Das **Data Secure-Badge** in der Statusleiste der Monitor-Seite spiegelt den aktuellen Zustand wider: Grau hinterlegt, wenn keine Data Secure-Gruppenadressen im geladenen Projekt vorhanden sind; Orange, wenn Data Secure-Adressen geladen, aber die Absender noch nicht konfiguriert wurden; und Grün, sobald die Absender konfiguriert und bereit zum Senden sind.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-data-secure/knx-data-secure-project-banner.png" width="320" alt="Projektseite mit dem Data Secure-Banner, das nach dem Laden eines Projekts mit Data Secure-Gruppenadressen zur Konfiguration der Absender auffordert" />
</div>

---

## Senden von Data Secure-Telegrammen — Die Absenderadresse

Wenn SharKNX einen Data Secure-Befehl sendet, muss die App eine Physikalische Adresse verwenden, die das Zielgerät als vertrauenswürdigen Absender anerkennt. Steht die Adresse nicht auf der Absenderliste des Geräts, wird der Befehl ignoriert.

SharKNX verwaltet dies über die Konfiguration der **Data Secure-Absender (Data Secure Senders)**. Diese erreichen Sie direkt über das Banner, das auf der Projektseite erscheint, sobald ein Projekt mit sicheren Gruppenadressen geladen wurde.

Auf der Absender-Seite können Sie:

- Eine **globale Absenderadresse** festlegen – diese wird für alle Data Secure-Gruppenadressen verwendet, für die keine spezifische Adresse definiert ist.
- **Adressspezifische Überschreibungen** einrichten – hiermit weisen Sie einzelnen Gruppenadressen ganz bestimmte Physikalische Absenderadressen zu.
- **Automatisch aus Projektdaten generieren** – SharKNX liest das ETS-Projekt aus und erstellt automatisch die Zuordnungen zwischen Gruppenadresse und Physikalischer Adresse basierend darauf, welche Geräte mit den jeweiligen sicheren Gruppenadressen verknüpft sind. Dies ist der schnellste Weg, die Absender bei einem vollständigen Projekt einzurichten.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/knx-data-secure/knx-data-secure-senders.png" width="320" alt="Konfigurationsseite für Data Secure-Absender mit globalem Absender und der Liste für adressspezifische Zuordnungen" />
</div>

---

## Die Einschränkung der Absenderadresse bei KNX IP Secure

Wenn SharKNX über einen **KNX-IP-Secure-Tunnel** verbunden ist, wird die Physikalische Adresse für alle ausgehenden Telegramme vom IP-Gateway fest vorgegeben (es ist die Adresse der zugewiesenen Tunneling-Schnittstelle). SharKNX kann diese Adresse nicht überschreiben – dies ist eine feste Eigenschaft des KNX-IP-Secure-Protokolls.

Daraus ergibt sich eine praktische Einschränkung: Damit ein Data Secure-Feldgerät Befehle von SharKNX über einen KNX-IP-Secure-Tunnel akzeptiert, muss die Adresse der Tunneling-Schnittstelle des Gateways bereits in der ETS auf der Liste der vertrauenswürdigen Absender des Feldgeräts stehen.

Zwei Lösungsansätze haben sich in der Praxis bewährt:

1. **Nutzung einer dedizierten Dummy-Schnittstelle in der ETS:** Erstellen Sie ein virtuelles sicheres Schnittstellengerät (z. B. KNX-Dummy) in Ihrem ETS-Projekt und verbinden Sie alle Data Secure-Gruppenadressen mit diesem. Tragen Sie dessen Physikalische Adresse als Absender in SharKNX ein. Dies trennt den Zugriff von SharKNX sauber von anderen Clients.
2. **Verknüpfen der Gruppenadressen mit den Tunnel-Schnittstellen des Gateways:** Verbinden Sie in der ETS die Data Secure-Gruppenadressen direkt mit den Tunneling-Schnittstellen Ihres KNX-IP-Secure-Gateways. Jeder Client, der sich über diese Schnittstelle verbindet (einschließlich SharKNX), wird dann von den Feldgeräten auf dem Bus als vertrauenswürdiger Absender erkannt.

> Wenn Sie die Verbindung ohne KNX IP Secure herstellen (Standard-Tunnel ohne Verschlüsselung), kann SharKNX jede beliebige von Ihnen konfigurierte Physikalische Adresse als Absender verwenden. Diese Einschränkung entfällt in diesem Fall.

---

## Tool-Schlüssel für das Gerätemanagement (Device Management)

KNX Data Secure gilt auch für administrative Geräteverwaltungs-Operationen – wie das Auslesen von Geräteinfos, das Umschalten des Programmiermodus, das Zurücksetzen eines Geräts, das Programmieren einer Physikalischen Adresse oder das Auslesen von Kommunikationstabellen. Geräte, die eine Authentifizierung auf Tool-Ebene erfordern, weisen Management-Befehle von unbekannten Quellen ab.

Wenn Sie eine `.knxkeys`-Datei im **Sicherheit-Tab** der Discovery-Seite laden, extrahiert SharKNX automatisch alle darin enthaltenen **Tool-Schlüssel (Tool Keys)** und speichert sie ab. Diese Schlüssel ermöglichen eine verschlüsselte Gerätemanagement-Kommunikation mit den entsprechenden Data Secure-Geräten – nach dem Laden der Schlüssel ist keine weitere Konfiguration erforderlich.

Tool-Schlüssel sind unabhängig von den in der `.knxproj`-Datei eingebetteten Gruppenschlüsseln. Wenn Ihre Installation Data Secure für das Gerätemanagement nutzt, benötigen Sie zusätzlich zum geladenen Projekt auf der Projektseite auch die `.knxkeys`-Datei (oder die `.knxproj`-Datei, die die Tool-Schlüssel ebenfalls enthält) im Sicherheit-Tab.

---

## Weiterführende Links

Für eine detaillierte technische Erklärung des KNX Data Secure-Protokolls ist das ABB-Anwendungsbeispiel "i-bus KNX Data Secure" eine hervorragende und tiefgehende Ressource. Es deckt die kryptografischen Mechanismen, die Verwaltung von Sequenznummern und die ETS-Konfiguration umfassend ab.

---

## KNX Data Secure vs. KNX IP Secure

| Merkmal | KNX Data Secure | KNX IP Secure |
|---|---|---|
| **Ebene** | KNX-Telegramm (Anwendungsebene) | IP-Transportebene |
| **Was wird verschlüsselt?** | Einzelne Gruppentelegramme auf dem KNX-Medium (TP/RF) | Der UDP/TCP-Tunnel oder der Multicast-Kanal |
| **Art der Zugangsdaten** | Gruppenschlüssel pro Gruppenadresse; Tool-Schlüssel pro Gerät | Schnittstellen-Zugangsdaten; Backbone-Schlüssel |
| **Wo in SharKNX konfiguriert?** | Projektseite (Schlüssel aus `.knxproj`); Sicherheit-Tab (Tool-Schlüssel) | Discovery-Seite $\rightarrow$ Sicherheit-Tab |
| **Erforderlich für...** | Senden/Empfangen von sicheren Gruppentelegrammen | Verbindung zu einem KNX-IP-Secure-Gateway |

Beide Mechanismen arbeiten unabhängig voneinander und können einzeln oder kombiniert eingesetzt werden. Das Gegenstück auf der Transportebene finden Sie unter [KNX IP Secure](knx-ip-secure.md).
