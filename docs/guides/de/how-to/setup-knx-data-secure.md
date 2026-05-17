# KNX Data Secure einrichten

KNX Data Secure verschlüsselt einzelne KNX-Telegramme direkt auf der Anwendungsschicht (Application Layer). Um verschlüsselte Telegramme korrekt zu empfangen und zu senden, benötigt SharKNX die Gruppenschlüssel aus Ihrem ETS-Projekt sowie – für den Sendevorgang – eine konfigurierte Absenderadresse. Diese Anleitung führt Sie durch beide Schritte.

Hintergrundinformationen zur Funktionsweise von KNX Data Secure finden Sie unter [KNX Data Secure (Konzepte)](../concepts/knx-data-secure.md).

---

## Voraussetzungen

- Eine `.knxproj`-ETS-Projektdatei, die KNX Data Secure-Gruppenadressen enthält.
- Eine freie Physikalische KNX-Adresse, die SharKNX als Absenderidentität nutzen kann. Diese Adresse muss im ETS-Projekt existieren und über die entsprechenden Zugriffsrechte für die Gruppenadressen verfügen, die Sie ansteuern möchten.

> **Einschränkung bei KNX IP Secure:** Das Senden von KNX Data Secure-Telegrammen erfordert, dass der Monitor über eine verschlüsselte KNX IP Secure-Tunnelverbindung läuft. Falls Ihr Gateway kein KNX IP Secure unterstützt, gibt es zwei Workarounds in der ETS – Details dazu finden Sie auf der Konzeptseite zu [KNX Data Secure](../concepts/knx-data-secure.md#sending-constraints).

---

## Teil 1 — Gruppenschlüssel laden

Die Gruppenschlüssel sind direkt in der `.knxproj`-Datei eingebettet. Es genügt, das Projekt zu laden – SharKNX extrahiert die Schlüssel vollautomatisch.

1. Wechseln Sie auf die Seite **Projekt**.
2. Tippen Sie auf den **Ordner-FAB**, um die Dateiauswahl zu öffnen, oder wählen Sie ein kürzlich geladenes Projekt aus der Verlaufsliste.
3. Wählen Sie Ihre `.knxproj`-Datei aus.
   - Falls das Projekt passwortgeschützt ist, geben Sie das Passwort bei der Abfrage ein.
4. Überprüfen Sie nach dem Laden das **Data Secure-Banner** oben auf der Projektseite. Wenn dieses erscheint, enthält das Projekt Data Secure-Gruppenadressen und die Schlüssel wurden erfolgreich geladen.

---

## Teil 2 — Die Absenderadresse konfigurieren

SharKNX muss wissen, welche Physikalische Adresse es beim Senden von Data Secure-Telegrammen verwenden soll. Ohne diese Angabe schlagen verschlüsselte Sendevorgänge fehl.

1. Tippen Sie auf der **Projektseite** auf das **Data Secure-Banner**. Dadurch öffnet sich das Konfigurationsmenü für die Absenderadresse.
   - Alternativ können Sie zu **Projekt $\rightarrow$ Reiter Geräte** navigieren, das Gerät suchen, dessen Adresse Sie als Absender nutzen möchten, und die Konfiguration von dort aus aufrufen.
2. Wählen Sie im Konfigurationsmenü einen der beiden folgenden Ansätze:

### Option A — Eine spezifische Physikalische Adresse konfigurieren

1. Tippen Sie auf **Absenderadresse hinzufügen**.
2. Geben Sie die Physikalische Adresse ein (z. B. `1.1.250`) oder tippen Sie auf das Lupe-Symbol, um ein Gerät direkt aus dem geladenen Projekt auszuwählen.
3. Bestätigen Sie die Eingabe. Die Adresse ist nun als vertrauenswürdiger Sender hinterlegt.

### Option B — Die globale (automatische) Absenderadresse nutzen

Wenn Sie die Physikalischen Adressen nicht für jede Gruppenadresse einzeln manuell zuweisen möchten:

1. Tippen Sie auf **Globale Absenderadresse festlegen**.
2. Geben Sie die Adresse ein, die für alle verschlüsselten Sendevorgänge standardmäßig genutzt werden soll.

SharKNX verwendet diese Adresse nun für jede Data Secure-Gruppenadresse, für die keine spezifische Absenderadresse konfiguriert ist.

> Wenn keine der beiden Optionen eine Adresse verwendet, die in der Liste der vertrauenswürdigen Sender des ETS-Projekts für die jeweilige Gruppenadresse hinterlegt ist, wird das empfangende Busgerät das Telegramm verwerfen. Stellen Sie sicher, dass die von Ihnen konfigurierte Adresse in der ETS zur Senderliste des Gruppenobjekts hinzugefügt wurde.

---

## Teil 3 — Überprüfung (Validierung)

1. Starten Sie den Monitor (verbinden Sie sich mit Ihrem Gateway und tippen Sie auf den Start-FAB auf der Monitor-Seite).
2. Lösen Sie ein Data Secure-Telegramm auf dem Bus aus – drücken Sie beispielsweise einen physischen Taster an der Wand.
3. Das Telegramm sollte in der Monitorliste mit vollständig dekodiertem Wert (nicht nur als Rohdaten) erscheinen. Dies bestätigt, dass der Gruppenschlüssel korrekt angewendet wurde.
4. Sendevorgang prüfen: Halten Sie im Monitor die Zeile eines Data Secure-Gruppenadressen-Telegramms gedrückt, um den Befehls-Editor aufzurufen (vorausgefüllt mit Adresse und DPT). Senden Sie einen Schreibbefehl (Write). Das Gerät sollte wie erwartet reagieren.

---

## Wichtige Hinweise

- Die Gruppenschlüssel werden bei jedem Laden eines Projekts neu eingelesen. Wenn die Schlüssel in der ETS neu generiert wurden (z. B. nach einer Teil-Inbetriebnahme oder einem Sicherheits-Update), laden Sie das Projekt einfach neu in die App, um die aktualisierten Schlüssel zu übernehmen.
- Konfigurierte Absenderadressen bleiben auch nach einem App-Neustart erhalten. Sie müssen diese Konfiguration pro Projekt nur ein einziges Mal vornehmen.
- Das Data Secure-Badge auf der Monitor-Seite und den Shark-Hunt-Seiten zeigt Ihnen den aktuellen Status auf einen Blick: **Gelb** bedeutet, dass die Absenderadressen noch konfiguriert werden müssen; **Grün** signalisiert Einsatzbereitschaft.
