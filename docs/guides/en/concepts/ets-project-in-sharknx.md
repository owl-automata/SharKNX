# ETS Projects in SharKNX

SharKNX can load a standard ETS project file (`.knxproj`) to enrich every part of the app with the names, datapoint types, and structure you already defined in ETS. This page explains what that means in practice — what SharKNX does with the file, what it does not do, and what to keep in mind.

---

## The Project File Is Never Modified

Loading a `.knxproj` file into SharKNX is a read-only operation. SharKNX reads the file once, extracts the data it needs, and stores it internally. **The original file on your device is never written to or changed.** You do not need to worry about SharKNX corrupting your project, creating version conflicts, or causing issues when you open the same project in ETS later.

---

## What Loading a Project Unlocks

Without a project, SharKNX still works — you can connect to a gateway, monitor the bus, and send commands using raw group addresses. Everything is functional but unnamed. Loading a project changes the experience significantly:

**Project page — four structured views:**
The Group Addresses, Devices, Topology, and Buildings tabs all populate with the data from your project, mirroring the structure you have in ETS. You can browse the full hierarchy, search across all names, and tap any group address to send a read or write command directly.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/ets-project-in-sharknx/ets-project-group-addresses.png" width="320" alt="Project page showing the group address tree with main groups, middle groups, and group addresses from a loaded ETS project" />
</div>

**Monitor page — named, decoded telegrams:**
Incoming telegrams are automatically matched to the loaded project. Each telegram row shows the group address name and a human-readable decoded value based on its datapoint type, instead of just a raw hex payload. The command composer uses the project to prefill the group address name and DPT when you tap a group address.

**KNX Data Secure — automatic key extraction:**
If your project contains KNX Data Secure group addresses, their group keys are extracted automatically. SharKNX uses them to decrypt incoming data secure telegrams in the monitor and to encrypt outgoing data secure commands. No separate credential import step is needed for group-level security. See [KNX Data Secure](knx-data-secure.md) for details.

---

## Communication Objects

When the **Load communication objects** setting is enabled (the default), SharKNX also parses and stores the communication objects for each device that has group addresses connected to it. This adds an additional layer of detail:

- In the Devices tab, you can open a dedicated communication objects page per device, showing all connected comm objects with their flags, sizes, functions, and linked group addresses.
- This is particularly useful for device diagnostics — you can see at a glance which comm objects are mapped to which group addresses and send test commands directly from that view.

<div align="center">
  <img src="../../../../assets/screenshots/guides/concepts/ets-project-in-sharknx/ets-project-comm-objects.png" width="320" alt="Communication objects page for a device showing object number, flags, function, size, and linked group addresses" />
</div>

Disabling this setting reduces memory usage, which can be relevant on devices with limited RAM or for very large projects. The rest of the project data (group addresses, topology, buildings) is still loaded normally.

---

## What SharKNX Does Not Do

SharKNX is a field tool, not a commissioning tool. There are things it deliberately does not do with the ETS project:

- **No parameter changes.** SharKNX cannot read or modify device parameters stored in the project. Only ETS can write parameters to devices.
- **No application program download.** SharKNX cannot program or flash devices with their application software. This remains exclusively within ETS.
- **No connection to an ETS server or license.** SharKNX reads the exported `.knxproj` file directly. It does not connect to ETS, does not require ETS to be running, and does not consume an ETS license.

**Programming individual addresses** is the one write operation SharKNX supports that relates to project data — but it writes directly to the physical device on the bus via KNX management communication, not to the `.knxproj` file. The project file itself remains unchanged.

---

## Keeping Project Data Current

SharKNX reads the project file at the moment you load it. If you subsequently make changes in ETS and export a new `.knxproj`, SharKNX will not pick up those changes automatically — you need to reload the updated file.

The **Apply project data** function in the Monitor page tune menu helps with this: after loading an updated project, you can apply the new names and datapoint types to telegrams already captured in the monitor list, without having to re-record a session.

---

## Supported Formats

| Format | Supported |
|---|---|
| `.knxproj` (ETS5) | ✅ |
| `.knxproj` (ETS6) | ✅ |
| Password-protected projects | ✅ (password prompted on import) |
| `.knxpkg` or other ETS formats | — |

Only one project can be loaded at a time. Loading a new project replaces the current one. Previously loaded projects are kept in a history list for quick reloading without browsing the file system again.
