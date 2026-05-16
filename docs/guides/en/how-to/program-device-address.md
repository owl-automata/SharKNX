# How to Program a Device Individual Address

SharKNX can program (write) a KNX individual address to a device directly from your phone or PC — without needing ETS or physical access to a laptop on site. Two methods are available: via the physical programming button, or via the device serial number (no button press required).

---

## Prerequisites

- Connected to a KNX gateway (see [Connect to a Gateway](connect-to-gateway.md)).
- The new individual address you want to assign, either known from your project or entered manually.

---

## Method A — Via the Programming Button

Use this when you have physical access to the device (or a colleague on site can press the button).

1. Go to **Management → Line Scan** tab.
2. Run a line scan on the relevant area/line (see [Scan a Bus Line](scan-bus-line.md)), then tap the device card you want to reprogram to open its detail sheet.
   - Alternatively, go to **Management → Devices** tab, enter the device's current individual address, and use the actions from there.
3. In the device detail sheet, tap **Program Address**.
4. Enter the new individual address in the input field, or tap the **search icon** to select one from your loaded ETS project.
5. Tap **Program via programming button**.
6. The app waits up to **20 seconds** for a device to enter programming mode. Press the programming button on the physical device during this window.
7. When the app detects a device in programming mode, it writes the new address and confirms success.

> The app checks whether the new address is already in use by another device on the real installation. If a conflict is detected, you are warned before the write is committed.

---

## Method B — Via Serial Number

Use this when you already have the device's serial number from a previous **Read Info** operation. No physical button press needed — ideal for devices in hard-to-reach locations.

1. First ensure the device's serial number is known: perform **Read Info** from the Line Scan device card or the Devices tab if you haven't already.
2. In the device detail sheet or Devices tab, tap **Program Address**.
3. Enter the new individual address, or select from the project.
4. Tap **Program via serial number**.
5. The app addresses the device directly using its serial number and writes the new address without requiring the programming button.

---

## Tip — Remote Programming Mode Toggle

If you cannot reach the programming button physically, use **Toggle Programming Mode** from the device card or Devices tab to enable it remotely first. Then immediately run **Program via programming button** — the app will detect it within the 20-second window. Toggle it off again afterwards.

---

## Notes

- After programming, verify the result by tapping **Check** on the device card to confirm the new address is active on the bus.
- This workflow supports the initial commissioning flow: scan the line → identify all devices → program addresses → connect and download programs from ETS.
