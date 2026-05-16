# How to Load an ETS Project

Loading a `.knxproj` file gives SharKNX access to group address names, datapoint types, device metadata, and KNX Data Secure keys. Without a project, the monitor shows only raw hex values with no names.

---

## Before You Start

The `.knxproj` file must already be on your device. If it is not, transfer it first:
- Share it from ETS directly to your phone via a messaging app, email, or AirDrop
- Save it to a cloud drive (iCloud, Google Drive, OneDrive) and open from there
- Transfer via USB

SharKNX supports `.knxproj` files from **ETS5 and ETS6**, including password-protected projects.

---

## Steps

1. Go to the **Project** page (second tab in the bottom navigation).
2. Tap the **folder FAB**.
   - If you have loaded projects before, a **history sheet** opens. Tap any entry to reload it instantly — no file browsing needed.
   - To load a new file, tap **Browse** (or the file picker button) to open the system file picker.
3. Select your `.knxproj` file.
4. If the project is **password-protected**, enter the password when prompted and confirm.
5. The project loads. The search bar, expand/collapse button, and the four tabs (Group Addresses, Devices, Topology, Buildings) become active.

---

## What Changes After Loading

- The **Monitor page** and **Shark Hunt monitor** will now show group address names and decoded values for incoming telegrams.
- The **Project page** search bar lets you filter all group addresses, devices, and building elements by name.
- If the project contains **KNX Data Secure** group addresses, a banner appears below the tab bar. Tap it to configure sender addresses before sending secured commands. See [Set Up KNX Data Secure](setup-knx-data-secure.md).

---

## Loading from Other Pages

You do not have to navigate to the Project page to load a project. The **ETS Project badge** on the Monitor page and on Shark Hunt pages has a **Load project** button when no project is currently loaded — tapping it opens the same history sheet and file picker.

---

## Updating or Replacing a Project

SharKNX holds one project at a time. To switch to a newer export or a different project:

1. Tap the **folder FAB** again on the Project page (or the ETS Project badge anywhere in the app).
2. Select the updated `.knxproj` file.
3. The new project replaces the previous one immediately.

> If the monitor is active when you load a new project, it will apply to new incoming telegrams. Telegrams already in the list keep the metadata from the previous project until the list is cleared.

To unload a project entirely without loading a new one, tap the **tune icon** on the Project page and select **Unload project**.

---

## Notes

- Loading the wrong project (one that does not match your physical installation) will result in incorrect group address names and decoded values in the monitor. Always verify you have the right project for the site you are working on.
- The project file is read once at load time. SharKNX does not stay connected to ETS and does not detect changes made in ETS after the file was loaded. Re-load the file after any ETS changes.
- SharKNX never modifies the `.knxproj` file.
