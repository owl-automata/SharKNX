# How to Inspect a Device's Communication Objects

The Inspect tab in the Management page reads a device's communication tables directly from its memory and reconstructs which communication objects exist, what flags they have, and which group addresses are connected to them — without needing an ETS project. This is the most reliable way to understand an unknown or incorrectly documented device.

---

## Prerequisites

- Connected to a KNX gateway (see [Connect to a Gateway](connect-to-gateway.md)).
- The individual address of the device you want to inspect.

---

## Steps

1. Go to **Management → Inspect** tab.
2. Enter the device's individual address in the input field.
   - You can also reach this tab pre-filled from the **Prog. Mode** tab (tap **Comm. Info** on a card), from a **Line Scan** device card (tap **Rebuild Communication**), or from any device detail sheet.
3. Tap **Read**. A progress bar shows which operation is in progress (address table, association table, communication objects).
4. A session card appears for the device. The border colour indicates success (green) or failure (red).

---

## Reading Full Device Info

The communication table read does not include detailed device info (manufacturer, firmware, etc.) by default. Tap **Read Full Info** on the session card to retrieve those details separately.

---

## Viewing Session Details

Tap the session card to open its full details page. The top bar has a **reload** button to re-run the read, and a **share** button to export and share a PDF report for this session.

The details page has three tabs:

### Associations

Lists all communication objects that have at least one group address connected:

| Column | Description |
|---|---|
| Number | Communication object index |
| Flags | R Read · W Write · C Communication · T Transmit · U Update · I Read-on-Init |
| Size | Object data size (1 bit, 1 byte, 2 bytes, etc.) |
| Group addresses | Addresses connected to this object |

Tap any group address to send a **Read** or **Write** command to it. Because the DPT is not known from memory alone, a raw hex/decimal value input is used instead of a DPT-aware UI.

Use **Export CSV** or **Export TXT** to export the associations list for this session.

### Device Info

Shows the full device info card if **Read Full Info** was performed. Includes a **Copy All** button to copy all fields to the clipboard.

### Addresses

A table of all group addresses found in the device's address table in memory (index, 3-level, 2-level, hex). Use **Copy All** or **Export CSV** to extract the full list.

---

## Managing Sessions

Sessions are **persistent** — they survive app restarts and remain available until you clear them.

- **Clear** (above the card list) — removes all sessions
- **Export** (above the card list) — exports all sessions together as a single PDF
- **Share** (top bar of a session details page) — exports and shares just that one session as PDF

---

## Notes

- A failed read (red border) usually means the device is not responding, is in an error state, or the address is wrong. Use **Check** from the Devices tab to verify the device is present on the bus first.
- If the device requires KNX Data Secure tool keys for device management operations, load the `.knxkeys` file in **Discovery → Security** tab before reading.
