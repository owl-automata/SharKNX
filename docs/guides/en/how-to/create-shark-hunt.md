# How to Create a Shark Hunt

A shark hunt is a reusable set of send actions and monitor filters saved as a portable file. This guide walks through the five-step creation wizard and explains how to configure each of the six available action types.

For an overview of what shark hunts are and how the hunt page works, see [Shark Hunts](../concepts/shark-hunts.md).

> The app supports up to **25 hunts**. Each hunt supports up to **25 actions**.

---

## The Creation Wizard

On the Shark Hunts main page, tap the **+ FAB** to open the wizard.

Every wizard step has:
- An **X button** (top left) to close — the app warns you about unsaved changes
- **Back / Next** buttons at the bottom to navigate between steps
- A **Save button** (top right) that appears as soon as you make any change, letting you save progress and exit to finish later

---

### Step 1 — Name and Description

Enter a **name** for the hunt (required) and an optional **description**. Toggle **Mark as favourite** if you want the hunt to appear first when you filter by star on the main page.

---

### Step 2 — ETS Project

Choose whether this hunt will use an ETS project:

| Option | When to use |
|---|---|
| **Use loaded ETS project** | A project is already loaded — the hunt will use its group addresses, devices, and building structure for action creation and monitor filters |
| **Load a project** | No project is loaded yet — opens the file picker so you can load one now |
| **Manual input** | You don't have or don't need a project — group addresses must be typed manually in action creation |

> **Monitor Space** and **Monitor Device** action types require an ETS project. If you skip project selection here, those two action types will not be available in Step 3.

---

### Step 3 — Actions

This is where you build the content of the hunt. Tap **Add action** and choose an action type from the list. See [Action Types](#action-types) below for full details on each type.

Created actions appear as cards. Each card has:
- **Edit** — reopen the action configuration
- **Copy** — duplicate the action (useful for similar actions with small differences)
- **Delete** — remove the action

Repeat until you have all the actions you need.

---

### Step 4 — Gateway (Optional)

Optionally embed a gateway configuration in the hunt. This lets the recipient of a shared hunt connect without needing to discover or configure the gateway themselves — ideal for sharing with non-expert users for remote diagnostics.

Select from already-discovered gateways or tap **Configure manually** to enter an IP address and port. This step can be skipped entirely if no embedded gateway is needed.

---

### Step 5 — Review and Create

A summary of all your selections. Review and tap **Create** to finish. The hunt appears on the main page as a card.

---

## Action Types

Each action creation page requires an **action name** (required) and an optional **description**. The **tick FAB** becomes active once all required fields are filled, and tapping it saves and creates the action.

---

### Send Fixed

Sends one fixed value to one group address every time the action is tapped.

1. Enter the group address, or tap the **search icon** to select one from the loaded ETS project (auto-fills the DPT).
2. Choose **Write** or **Read**.
3. Select the **DPT** type and subtype.
4. For Write: enter the value to send (e.g. On, 75%, 21.5°C, Scene 3).
5. Tap the **tick FAB** to save.

**Examples:** Toggle a light on, set a thermostat setpoint, recall a scene, test a shutter position.

---

### Send Multiple / Sequence

Sends a list of fixed commands in sequence, optionally with delays between them.

1. Tap the **+ button** to add the first command — the command composer opens. Enter the group address, DPT, read/write, and value, then tap the tick FAB to add it.
2. Tap **+** again to add more commands (up to **15**).
3. Each command appears as an expandable card showing the DPT and value.
4. To add a delay before a command: tap the **"Immediate"** subtitle on a card and enter a delay in seconds (max **10 s**). The next command will wait that long before executing.
5. To reorder: tap the **six-dot drag handle** on any card and drag it to the desired position.
6. Tap the **tick FAB** to save the action.

**Example:** Set scene → wait 2 s → read status → wait 1 s → send confirmation.

---

### Send Variable

Sends a value you choose at run time to one or more group addresses. Useful when you need to test different values on the same address or broadcast to several related addresses at once.

1. Enter a group address in the input field and tap **Add**. Repeat for each target address (up to **15**).
   - Use the **project search** to multi-select group addresses from the loaded ETS project at once.
2. All added addresses must share the same DPT. Mismatches are highlighted on the address cards but do not block creation — just be aware that the device may not respond as expected.
3. Tap the **tick FAB** to save.

When you run this action in the hunt page, a bottom sheet opens with a DPT-appropriate value input. Enter the value and confirm to send to all target addresses.

**Examples:** Select all thermostat setpoint group addresses in a floor and send 21 °C in one tap to verify that every HVAC zone responds correctly. Or target all dimmer channel addresses in a room and sweep through brightness values to find the one causing flicker.

---

### Custom Monitor

Creates an advanced filter for a monitor session using one or more conditions combined with AND / OR logic.

1. Tap the **+ button** to add a condition. Up to **10 conditions** can be added.
2. Choose the condition type:

   | Condition | What it filters |
   |---|---|
   | **Group address** | Show only telegrams to/from specific group addresses. Enter addresses manually or select from the project. Supports wildcards (`1/*/*`, `1/*/0`). Toggle **Exclude** to invert (show everything except these addresses). |
   | **Device address** | Show only telegrams from specific individual addresses. Manual input or project search. Supports wildcards (`1.*.*`). Toggle **Exclude** to invert. |
   | **Telegram type** | Filter by APCI type: Write, Read, Response, or any combination. |
   | **Text search** | Show only telegrams whose group address name or description contains a search string. Requires a loaded ETS project. |
   | **Timestamp** | Show telegrams before, after, or between specific times. Useful for testing time-based automation. |

3. After adding conditions, set the **logic operator** between them: **AND** (all conditions must match) or **OR** (any condition must match).
4. Tap the **tick FAB** to save.

**Examples:**
- *Isolate a suspected device:* Add a Device Address condition for the suspected sender AND a Group Address condition for the affected GA range. Only telegrams from that device to those addresses appear — everything else is filtered out.
- *Verify a morning automation:* Add a Timestamp condition (after 07:00) AND a Telegram Type condition (Write only). Run the monitor the next morning and confirm the scheduler fired the right commands at the right time.
- *Monitor everything except your own test traffic:* Add a Device Address condition with **Exclude** for your laptop or phone's individual address, so only real installation traffic is shown while you test.

---

### Monitor Space

Quickly creates a monitor filter scoped to a physical space in your ETS building structure. Requires an ETS project (set in Step 2).

1. Choose what to monitor:
   - **Group addresses** — monitor all group addresses assigned to devices in the selected space
   - **Device senders** — monitor all individual addresses of devices in the selected space
2. Tap **Select space** — your ETS building structure appears as a sheet. Select a floor, room, or any location (e.g. Kitchen, Living Room).
3. Tap the **tick FAB** to save.

> Up to **750 addresses** can be captured from a single space selection. Large spaces with many devices may approach this limit.

---

### Monitor Device

Creates a monitor filter scoped to one or more specific devices in your ETS project. Requires an ETS project (set in Step 2).

1. Tap **Select devices** — your project's device list appears. Select one or more devices.
2. The filter will monitor all group addresses connected to the selected devices.
3. Tap the **tick FAB** to save.

> The same **750-address** limit applies. Useful for testing communication between two devices or verifying all outputs of a controller.

---

## Editing an Existing Hunt

From the main page, tap the **three-dot menu** on any hunt card and select **Edit**. This reopens the wizard with all existing data. You can change the name, add or remove actions, change the gateway, or update any other setting.

---

## Sharing a Hunt

From the three-dot menu, tap **Share** to send the hunt as a JSON file via any share target (email, messaging app, cloud drive). The recipient imports it via the **tune icon → Import Hunts** on their Shark Hunts page. A single exported file can contain one or multiple hunts.
