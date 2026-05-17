# Project Page

The Project page is the second page in the bottom navigation bar. It is where you load an ETS project file and browse its contents across four structured views: Group Addresses, Devices, Topology, and Buildings.

---

## Loading a Project

Tap the **folder FAB** to open the file picker and select a `.knxproj` file. If you have loaded projects before, a history sheet appears first — select a recent entry or tap **Browse** to pick a new file. Password-protected projects are supported; the app prompts for the password during import.

Loading a new project replaces the currently loaded one. The previously loaded project's data is cleared from memory.

> For background on what loading a project does and does not do, see [ETS Projects in SharKNX](../concepts/ets-project-in-sharknx.md).

---

## Search and Filter Bar

Once a project is loaded, a search and filter bar appears below the tab bar. Type any text to search across all names in the project — group addresses, devices, buildings, lines, and functions. Results update as you type across whichever tab is active.

Next to the search bar is an **Expand All / Collapse All** button that expands or collapses all tree sections in the current tab at once.

---

## KNX Data Secure Banner

If the loaded project contains KNX Data Secure group addresses, a banner appears below the tab bar prompting you to configure Data Secure senders. Tapping the banner navigates to the Data Secure Senders configuration page, where you set which individual address SharKNX should use as the sender for each secure group address. This is required for sending Data Secure commands; monitoring works without this step. See [KNX Data Secure](../concepts/knx-data-secure.md) for details.

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-data-secure-banner.png" width="320" alt="Project page with the data secure banner below the tab bar after loading a project with secure group addresses" />
</div>

---

## Group Addresses Tab

This tab shows the group address hierarchy as you have it in ETS: main groups at the top level, expanding to middle groups, expanding to individual group addresses.

Tap any main or middle group to expand or collapse it. Tap any **group address** to open its quick action sheet, which shows:
- Group address name
- Datapoint type and subtype
- **Read** button — sends a read request to the bus and displays the response inline in the sheet within 1 second if a response arrives
- **Write** button — opens the command composer with the group address and DPT prefilled; enter a value and send

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-group-addresses.png" width="320" alt="Group Addresses tab showing the main group tree expanded to individual group addresses" />
</div>

> A gateway must be selected to send read or write commands. If none is selected, the app prompts you to choose one.

---

## Devices Tab

This tab lists all devices in the project ordered by individual address. Devices that have group addresses connected to them can be expanded to show those addresses — tap any of them to open the same quick action sheet as in the Group Addresses tab.

**Tap** a device with no group addresses, or **long-press** a device with group addresses, to open the **device detail sheet**. This sheet contains:

### Device Info Card
A compact card showing whether the device's individual address and application program are loaded in the ETS project.

### Quick Diagnostic Actions

| Action | What it does |
|---|---|
| **Check** | Checks if the device is present and responsive on the bus |
| **Read Info** | Reads detailed device information directly from the device (see below) |
| **Toggle Programming Mode** | Turns the device's programming mode on or off remotely |
| **Program Address** | Scans for a device in programming mode and writes a new individual address to it |

**Read Info** retrieves the following from the device:
- Device descriptor (e.g. System B)
- Programming mode status
- Manufacturer and order number
- Firmware version
- Load state and run state
- Application version
- Address table and association table status
- Max APDU length
- Hardware type
- Error flags and device status

### Communication Objects Button

Opens the dedicated **Communication Objects page** for this device (see below).

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-device-detail.png" width="320" alt="Device detail bottom sheet showing the info card, four quick action buttons, and the Communication Objects button" />
</div>

---

## Communication Objects Page

Accessible from the Communication Objects button in the device detail sheet. This page shows all communication objects for the device that are connected to at least one group address.

At the top, the page shows the device's **last modified** and **last downloaded from ETS** dates.

Each communication object entry shows:
- Object number
- Flags: Read, Write, Communication, Transmit, Update, Read-on-Init
- Function name (if available in the device application)
- Object size (e.g. 1 bit, 1 byte, 2 bytes)
- Connected group addresses — each is tappable to open the quick action sheet for read/write commands

<div align="center">
  <img src="../../../../assets/screenshots/guides/pages/project/project-comm-objects.png" width="320" alt="Communication Objects page showing a list of comm objects with flags, size, and linked group addresses" />
</div>

> The **Load communication objects** setting in Project Settings controls whether this data is parsed at load time. It is enabled by default. Disabling it reduces memory usage for large projects but removes access to this page.

---

## Topology Tab

This tab shows the physical topology of the project: areas at the top level, expanding to lines or segments, then to devices. Tap any device to open the same device detail sheet described above.

---

## Buildings Tab

This tab shows the building structure as configured in ETS: buildings and floors expanding to rooms and functions, with group addresses and devices underneath. Tap any group address or device to open their respective quick action sheets.

---

## Tune Menu

The tune icon in the top bar opens a bottom sheet with one action:

**Unload project** — removes the currently loaded project from memory. All four tabs return to their empty state. Captured telegrams in the Monitor page remain but lose their names and decoded values.
