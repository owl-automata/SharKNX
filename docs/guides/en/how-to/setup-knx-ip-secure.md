# How to Set Up KNX IP Secure

KNX IP Secure encrypts the tunnel connection between SharKNX and your gateway using AES-128 CCM over TCP. Before SharKNX can connect to a secure gateway, it needs the matching credentials. This guide explains how to load them.

For background on what KNX IP Secure protects and how it works, see [KNX IP Secure](../concepts/knx-ip-secure.md).

---

## What You Need

One of the following credential sources (all produced by ETS):

| Format | How to obtain |
|---|---|
| `.knxkeys` keystore file | Export from ETS: Project → Security → Export keystore |
| `.knxproj` ETS project file | The same project file used to load group addresses; already contains device credentials |
| Backbone key (hex string) | Found in ETS under the interface's IP Secure settings |

---

## Step 1 — Open the Security Tab

1. Go to the **Discovery** page.
2. Tap the **Security** tab.

---

## Step 2 — Load Credentials

Three methods are available. Use whichever matches what you have:

### Method A — Load a `.knxkeys` keystore file

1. Tap **Load .knxkeys file**.
2. Select the `.knxkeys` file from your device storage.
   - If the file is password-protected, enter the keystore password when prompted.
3. A summary card appears confirming how many interface credentials were loaded.

### Method B — Load credentials from an ETS project file

If you already have a `.knxproj` file loaded or available:

1. Tap **Load from ETS project**.
2. Select the `.knxproj` file (or confirm the already-loaded project).
   - If the project is password-protected, enter the project password when prompted.
3. Credentials are extracted from the project file and loaded automatically.

### Method C — Enter a backbone key manually

1. Tap **Enter backbone key**.
2. Paste or type the 32-character hex backbone key.
3. Confirm. The key is saved and will be used for any gateway that requires it.

---

## Step 3 — Verify the Gateway Card

1. Go to the **Discover** tab and scan for gateways, or open the **Config** tab if your gateway is already saved.
2. Locate your secure gateway. Its card should show a **lock icon** indicating KNX IP Secure is supported.
3. If credentials were loaded successfully, the lock icon appears filled/active. If the icon is empty or the gateway card shows a credential warning, repeat Step 2 with the correct file.

---

## Step 4 — Connect

1. Tap **Select** on the gateway card to set it as the active gateway.
2. Start the monitor (or connect from a shark hunt page). SharKNX will automatically use the TCP secure tunnel.
3. If the connection succeeds, the connection badge turns green and telegrams begin flowing normally.

If the connection fails with a security error, the most common causes are:
- Wrong keystore file (credentials for a different gateway)
- Incorrect keystore or project password
- The gateway's tool key was rotated in ETS after the keystore was exported — re-export the keystore from ETS and reload

---

## Notes

- Credentials loaded via `.knxkeys` or `.knxproj` are stored on-device and persist across app restarts. You do not need to reload them each session.
- If a `.knxkeys` file contains tool keys for individual devices (used for device management operations), those are also loaded at this step and will be available in the Management and Project pages.
- You can view the history of previously loaded credential files in the Security tab.
- To use a different keystore, simply load the new file — it replaces the previous credentials.
