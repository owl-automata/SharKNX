# How to Set Up KNX Data Secure

KNX Data Secure encrypts individual KNX telegrams at the application layer. To receive and send secured telegrams correctly, SharKNX needs the group keys from your ETS project and, for sending, a configured sender address. This guide walks through both steps.

For background on how KNX Data Secure works, see [KNX Data Secure](../concepts/knx-data-secure.md).

---

## Prerequisites

- A `.knxproj` ETS project file that includes KNX Data Secure group addresses.
- A KNX individual address that SharKNX can use as its sender identity. This address must exist in the ETS project and have access rights to the group addresses you intend to send to.

> **KNX IP Secure constraint:** KNX Data Secure sending requires the monitor to be running over a KNX IP Secure tunnel. If your gateway does not support KNX IP Secure, two ETS workarounds exist — see the [KNX Data Secure](../concepts/knx-data-secure.md#sending-constraints) concept page for details.

---

## Part 1 — Load Group Keys

Group keys are embedded in the `.knxproj` file. Loading the project is enough — SharKNX extracts the keys automatically.

1. Go to the **Project** page.
2. Tap the **folder FAB** to open the file picker, or select a recently loaded project from the history list.
3. Select your `.knxproj` file.
   - If the project is password-protected, enter the password when prompted.
4. Once loaded, check the **Data Secure banner** at the top of the Project page. If it appears, the project contains Data Secure group addresses and the keys have been loaded.

---

## Part 2 — Configure the Sender Address

SharKNX needs to know which KNX individual address to use when sending Data Secure telegrams. Without this, secured sends will fail.

1. From the **Project** page, tap the **Data Secure banner**. This opens the sender configuration sheet.
   - Alternatively, navigate to **Project → Devices tab**, find the device whose address you want to use as the sender, and access sender configuration from there.
2. In the sender configuration sheet, choose one of two approaches:

### Option A — Configure a specific individual address

1. Tap **Add sender address**.
2. Enter the individual address (e.g. `1.1.250`), or tap the search icon to select a device from the loaded project.
3. Confirm. The address is saved as a trusted sender.

### Option B — Use the global (automatic) sender address

If you prefer not to specify individual addresses manually:

1. Tap **Set global sender address**.
2. Enter the address to use for all secured sends.

SharKNX will use this address for any Data Secure group address that does not have a specific sender address configured.

> If neither option has an address that appears in the ETS project's trusted sender list for a given group address, the receiving device will reject the telegram. Make sure the address you configure was added to the group object's sender list in ETS.

---

## Part 3 — Verify

1. Start the monitor (connect to your gateway and tap the start FAB on the Monitor page).
2. Trigger a Data Secure telegram on the bus — for example, press a switch.
3. The telegram should appear in the monitor list with its value decoded (not raw only). This confirms the group key was applied correctly.
4. To verify sending: from the monitor, long-press a Data Secure group address telegram row to open the command composer pre-filled with its address and DPT. Send a write command. The device should respond as expected.

---

## Notes

- Group keys are re-read each time you load a project. If ETS keys were rotated (e.g. after a recommission), reload the project to pick up the updated keys.
- Sender addresses persist across app restarts. You only need to configure them once per project.
- The Data Secure badge on the Monitor page and Shark Hunt pages shows the current sender status at a glance — amber means senders are not yet configured, green means ready.
