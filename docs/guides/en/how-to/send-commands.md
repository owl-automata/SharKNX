# How to Send KNX Commands

SharKNX can send both write and read commands to any KNX group address while monitoring is active. This guide covers the command composer, all the entry points that open it, and how to use quick-send chips for repeated commands.

---

## Prerequisites

- A gateway selected and the monitor running (see [Connect to a Gateway](connect-to-gateway.md)).
- Optionally, an ETS project loaded so group address names and DPTs are pre-filled automatically.

---

## The Command Composer

The command composer is the core send interface. It has four fields:

| Field | Description |
|---|---|
| **Group address** | The destination KNX group address. Type manually (e.g. `1/2/3`) or tap the search icon to browse your loaded ETS project |
| **Command type** | **Write** to send a value, **Read** to request the current value |
| **DPT** | Datapoint type and subtype (e.g. DPT 1.001 — Switch). Auto-filled if the address is selected from project data |
| **Value** | For write commands: the value to send, presented as a DPT-appropriate input (toggle, slider, colour picker, number field, etc.) |

Tap **Send** to transmit the command. It immediately appears in the monitor telegram list.

---

## Entry Points

### From the Monitor Page (Main Method)

1. Start the monitor — the green start FAB turns into a red **send FAB**.
2. Tap the **send FAB**.
3. A bottom sheet opens. Tap **New command** to open the command composer.
4. Fill in the fields and tap **Send**.

### Quick-Send Chips

After sending a command, a **chip** appears in the bottom sheet showing the group address and value. These chips persist for the session.

- **Tap a chip** to instantly resend the same command without reopening the composer.
- **Long-press a chip** to reopen the command composer with the group address and DPT already filled in — useful for resending with a different value.

### From a Telegram in the Monitor List

1. Tap any telegram row to open its detail sheet.
2. Tap **Write** — the command composer opens with the group address and DPT pre-filled from the telegram.
3. Enter a value and tap **Send**.

The detail sheet also has a **Read** button that sends a read request immediately without opening the composer.

### From the Project Page — Group Addresses Tab

1. Go to the **Project** page → **Group Addresses** tab.
2. Navigate the tree and tap any individual group address.
3. In the bottom sheet, tap **Write** to open the command composer pre-filled with the address and DPT, or tap **Read** to send a read command immediately.

### From the Project Page — Devices Tab

1. Go to the **Project** page → **Devices** tab.
2. Expand a device and tap any group address listed under it.
3. The same bottom sheet appears — tap **Write** or **Read**.

### From the Communication Objects Page

1. Go to the **Project** page → **Devices** tab.
2. Tap a device (or long-press a device that has group addresses) to open its detail sheet.
3. Tap **Communication Objects** to open the comm objects page for that device.
4. Tap any group address shown under a communication object — the same Read/Write bottom sheet appears, pre-filled with the address and DPT.

### From the Inspect Tab — Associations

When you have reconstructed a device's communication tables in the **Management → Inspect** tab, the Associations tab lists all group addresses found in device memory.

1. Tap any group address in the Associations tab.
2. Because the DPT is not available from device memory alone, a **raw value input** is shown instead of a DPT-aware UI. Enter a hex or decimal value and send.
3. A **Read** button is also available to send a read request to that address.

---

## Sending a Read Command

A read request asks the device currently holding the state of a group address to respond with its current value. The response telegram will appear in the monitor list. If the app was already monitoring when you tapped **Read** from the Project page, it listens for a response to that address for approximately one second and shows the result inline in the bottom sheet.

---

## Notes

- Sending is only possible while the monitor is running. Action cards in Shark Hunts are the exception — they connect and send independently per hunt.
- If you have a KNX Data Secure group address, the sender address must be configured before secured writes will be accepted by the device. See [Set Up KNX Data Secure](setup-knx-data-secure.md).
- Commands you send appear in the monitor list like any other telegram, so you can immediately see whether the bus acknowledged them.
