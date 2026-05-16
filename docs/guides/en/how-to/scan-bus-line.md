# How to Scan a KNX Bus Line

A bus line scan probes every individual address on a KNX line and lists all devices that respond. This lets you verify what is actually installed — independent of any ETS project — and is the fastest way to get an overview of an unknown installation.

---

## Prerequisites

- Connected to a KNX gateway (see [Connect to a Gateway](connect-to-gateway.md)).
- Know the KNX area and line number you want to scan (e.g. area 1, line 1 → `1.1`).

---

## Steps

1. Go to **Management → Line Scan** tab.
2. In the **Scan Settings** card, configure the scan:

   | Setting | Description |
   |---|---|
   | **Area / Line** | The area and line to scan (e.g. `1.1`). Tap **Choose from project** to select a line from your loaded ETS project — this also sets the medium type automatically. |
   | **Medium type** | TP, IP, or IoT. Must match the physical medium of the line. |
   | **Range** | Start and end device address within the line (0–255). Narrow this to speed up the scan or check a specific segment. |

3. Tap the **scan FAB** to start. The scan can be stopped at any time.
4. Discovered devices appear as cards. The top border colour indicates the device type:

   | Colour | Type |
   |---|---|
   | Blue | KNX coupler |
   | Red | Standard application device |
   | Green | KNX Secure device |

---

## Reading Device Info for All Discovered Devices

After the scan completes, tap **Read Device Info** (above the card list). The app reads manufacturer, serial number, and other details for each discovered device in sequence.

This is useful for:
- Quickly building an inventory of an installation you didn't commission
- Cross-referencing against an ETS project to verify it matches the physical installation
- Finding devices with unexpected addresses or types

---

## Working with Individual Device Cards

Tap any card to open its detail sheet. From there you can:

- **Check** — verify the device is still responsive
- **Read Info** — read full device details (manufacturer, firmware, run state, etc.)
- **Toggle Programming Mode** — enable or disable programming mode remotely
- **Restart** — send a restart command
- **Program Address** — assign a new individual address (see [Program a Device Individual Address](program-device-address.md))
- **Rebuild Communication** — opens the Inspect tab pre-filled with this device's address to read its communication tables

---

## Exporting Scan Results

Tap the **tune icon** in the top bar to export the most recent scan result:
- **Export as text** — TXT report with scan timestamp, gateway, area/line, medium, and device list
- **Export as PDF** — same content in PDF format
