# Getting Started with SharKNX

SharKNX is a professional KNX field companion for mobile and desktop. This guide walks you through the core workflow: connecting to a KNX IP gateway, loading an ETS project, and starting a live bus monitor session.

## Prerequisites

- A device running Android, iOS, Windows, or macOS 13+
- A KNX IP gateway reachable on the same IP network as your device
- (Recommended) An ETS project file (`.knxproj`) for your installation

> **Subscription:** SharKNX requires an active subscription. A 2-day free preview is available on first install without sign-up. Monthly and yearly plans include a 14-day free trial. A lifetime plan is also available as a one-time purchase. See [Subscription Plans](reference/subscription-plans.md) for details.

---

## Step 1 — Discover Your Gateway

The **Discovery** page opens automatically when the app starts. It is the leftmost page in the bottom navigation bar.

1. Tap the **scan FAB** at the bottom of the page.  
   The app sends KNX IP search requests across your local network. Any KNX IP gateways that respond appear as cards in the list.

2. Tap **Select** on the gateway card you want to use.  
   The gateway moves to the **Last Selected Gateway** section at the top of the page and is remembered across restarts — no need to scan again on the next session.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-discovery.png" width="320" alt="Discovery tab showing a discovered gateway card with Select and Save buttons" />
</div>

> **No gateways found?** Verify your device is on the same network segment as the gateway. On Wi-Fi with a wired VLAN, multicast packets may be dropped by the router. Use the **Config** tab to add the gateway manually by IP address and port, or enable **Force unicast subnet scan** in Discover Settings.

> **KNX IP Secure?** If your gateway requires KNX IP Secure credentials, tap the gateway card and use the **Load Credentials** button. See [Set Up KNX IP Secure](how-to/setup-knx-ip-secure.md) for the full procedure.

> **Save for later:** Tap **Save** on a gateway card to store it permanently in the **Config** tab. Saved gateways are available without re-scanning, which is useful when revisiting the same installation.

---

## Step 2 — Load Your ETS Project

An ETS project gives SharKNX the group address names, datapoint types, and device metadata for your installation. Without it, telegrams appear as raw hex values with no names or decoded values.

1. Tap the **Project** page (second tab in the bottom navigation bar).
2. Tap the **folder FAB** to open the file picker. Navigate to your `.knxproj` file and select it.  
   If you have loaded projects before, a history sheet appears first — select a recent entry or tap **Browse** to pick a new file.
3. Wait for the project to finish loading. The four tabs (Group Addresses, Devices, Topology, Buildings) populate with your project data.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-load-project.png" width="320" alt="Project page with the group address tree expanded after loading an ETS project" />
</div>

> **Getting the file onto your device:** Export your ETS project from your PC (`File → Export project` or right-click the project in ETS). Then transfer the `.knxproj` to your mobile using any method that suits you — send it to yourself via a messaging app (e.g. save to your own chat in Viber, WhatsApp, or Telegram), attach it to an email, upload it to a cloud drive (Google Drive, iCloud, OneDrive) and open it on your phone, or copy it over USB.

> **Password-protected projects** are supported. The app prompts for the project password during import.

> **Skipping this step:** You can monitor the bus without a project. Telegrams show only raw source and destination addresses with hex payloads.

---

## Step 3 — Start the Bus Monitor

1. Tap the **Monitor** page (fourth tab in the bottom navigation bar).
2. Tap the green **start FAB**.
   - If no gateway is selected yet, a picker appears listing your discovered and saved gateways — select one to proceed.
   - The app connects to the gateway and begins receiving telegrams.
3. Incoming telegrams appear as rows in the list. Each row shows:
   - Sender individual address → destination group address
   - Group address name and decoded value *(requires an ETS project)*
   - Raw hex payload
   - Timestamp in `HH:MM:SS.ms` format

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-monitor-active.png" width="320" alt="Monitor page with live telegrams in the list view" />
</div>

> Tap any telegram row to open its details, including source, destination, decoded value, and buttons to send an immediate **Read** or **Write** command to that address.

> **Keep screen on:** The monitor stops if the screen locks on mobile. Screen-on mode is enabled by default in Monitor Settings to prevent this.

---

## Step 4 — Send a Command

With the monitor running, you can send test commands without leaving the monitor view.

1. Tap the red **send FAB** (it replaces the start FAB once the monitor is active).
2. Tap **New Command** in the bottom sheet.
3. In the command composer:
   - Enter a group address, or tap the **search icon** to browse group addresses from your loaded project.
   - Choose **Write** or **Read**.
   - Select the datapoint type and subtype.
   - For write, enter the value to send.
4. Tap **Send**. The command is transmitted to the bus and appears in the telegram list immediately.

<div align="center">
  <img src="../../../assets/screenshots/guides/getting-started/getting-started-send-command.png" width="320" alt="Command composer page showing group address input, DPT selector, and value field" />
</div>

> **Quick resend:** After sending a command, a chip with its address and value appears near the send FAB. Tap the chip to resend immediately, or long-press it to reopen the composer with the fields pre-filled.

---

## What's Next

You now have a live monitor session, a named ETS project loaded, and know how to send test commands. From here:

| Goal | Guide |
|---|---|
| Browse group addresses and send commands from the project tree | [Project Page](pages/project.md) |
| Create reusable command and filter sets | [Shark Hunts](concepts/shark-hunts.md) |
| Set up KNX Data Secure group address decryption | [Set Up KNX Data Secure](how-to/setup-knx-data-secure.md) |
| Scan a bus line and check device presence | [Scan Bus Line](how-to/scan-bus-line.md) |
| Export your monitor session to CSV or PDF | [Export Formats](reference/export-format.md) |
| Read device firmware info or toggle programming mode | [Inspect Device](how-to/inspect-device.md) |
