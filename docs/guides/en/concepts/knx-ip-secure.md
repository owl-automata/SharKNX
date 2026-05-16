# KNX IP Secure

KNX IP Secure is the transport-layer security extension to the KNXnet/IP protocol. It encrypts communication between a KNX IP device (gateway or router) and a client such as SharKNX, preventing eavesdropping and unauthorized control over the IP network.

> This page explains what KNX IP Secure is and how SharKNX handles it. For the step-by-step setup procedure, see [Set Up KNX IP Secure](../how-to/setup-knx-ip-secure.md).

---

## What KNX IP Secure Protects

In a standard KNXnet/IP installation, tunneling traffic between a client and a gateway travels as unencrypted UDP packets. Anyone with access to the network can capture telegrams or inject arbitrary commands. KNX IP Secure addresses this by switching the tunneling transport to **TCP** and applying AES-128 CCM encryption to the session, ensuring that:

- Only clients with the correct credentials can establish a connection
- Traffic cannot be read or replayed by other parties on the network
- The gateway can reject connection attempts from unknown sources

KNX IP Secure operates at the IP transport layer. It does not change the KNX telegram content itself — that is the role of [KNX Data Secure](knx-data-secure.md).

---

## Two Modes of KNX IP Secure

### Secure Tunneling

Secure tunneling establishes an encrypted **TCP** connection between SharKNX and a KNX IP Secure-capable interface (typically a KNX IP gateway or the tunneling interface of a KNX IP router), replacing the UDP transport used by standard KNXnet/IP tunneling. Each tunneling connection has its own interface individual address and a corresponding set of credentials in the keyring.

**Sender address constraint:** When connected via a KNX IP Secure tunnel, the individual address used in outgoing telegrams is fixed to the tunneling interface address assigned by the gateway. SharKNX cannot override this. This matters when working with KNX Data Secure group addresses, which validate the sender's individual address — see [KNX Data Secure](knx-data-secure.md) for details.

### Secure Multicast (IP Routing Secure)

KNX IP routers that support IP Routing Secure use a shared symmetric key — the **backbone key** — to encrypt multicast traffic on the `224.0.23.12` multicast group over **UDP**. All participants on the backbone must use the same key.

SharKNX supports secure multicast. When a KNX IP Router is discovered, the **Discover** tab shows both a standard multicast option and a secure multicast option. Selecting the secure multicast option requires the backbone key to be loaded.

---

## Credential Files

KNX IP Secure credentials are distributed through ETS as part of the project keyring. SharKNX accepts credentials in three forms:

| Format | What it contains | Notes |
|---|---|---|
| `.knxkeys` | Interface credentials, backbone key, tool keys | Encrypted with a project-specific password set in ETS |
| `.knxproj` | Full ETS project including embedded keyring | SharKNX extracts the credentials automatically |
| Manual backbone key | Single symmetric key, entered as hex | For secure multicast only; use when you have only the key and not the full keyring file |

**Exporting `.knxkeys` from ETS:** Open your project in ETS. From the project overview (outside the project editor), go to **More details → Security**, then choose **Backup keyring**. Set a password and save the file.

> **Password validation:** SharKNX cannot verify whether a `.knxkeys` password is correct at the time of import — this is a property of the KNX specification. The password is only validated during the actual connection attempt. If the connection fails with an authentication error, check that the password matches what was set during the ETS keyring export.

---

## Where to Load Credentials in SharKNX

Credentials can be loaded in three places:

**Security tab (Discovery page):** The dedicated tab for managing all secure credentials. Tap the shield FAB to open the credential import sheet. After loading, the tab shows an overview of what was imported: how many interfaces were found and how many KNX Data Secure devices were present in the file. A history button lets you quickly reload recently used files.

<img src="../../../../assets/screenshots/guides/concepts/knx-ip-secure/knx-ip-secure-security-tab.png" width="320" alt="Security tab showing a loaded credential file with interface and device counts" />

**Gateway card (Discovery tab):** If a discovered gateway advertises KNX IP Secure support, its detail sheet includes a **Load Credentials** button. Credentials loaded here are stored the same way as through the Security tab.

<img src="../../../../assets/screenshots/guides/concepts/knx-ip-secure/knx-ip-secure-gateway-card.png" width="320" alt="Gateway detail bottom sheet with Load Credentials button for a KNX IP Secure gateway" />

**Discovery page tune menu:** The tune icon in the top bar of the Discovery page provides quick access to load credentials from a `.knxkeys` or `.knxproj` file without navigating to the Security tab.

Credentials are stored persistently and remain available across app restarts. Loading a new file replaces the previously stored credentials.

---

## KNX Data Secure Tool Keys

When a `.knxkeys` file contains tool keys for KNX Data Secure devices, SharKNX automatically stores those keys as well. This enables encrypted device management operations — such as toggling programming mode, reading device info, resetting a device, or reading communication tables — on devices that require tool-level authentication. These are separate from the IP Secure tunnel credentials and are used for device-level communication over KNX TP.

---

## KNX IP Secure vs. KNX Data Secure

| | KNX IP Secure | KNX Data Secure |
|---|---|---|
| **Scope** | IP transport layer | KNX telegram (application layer) |
| **What it encrypts** | The UDP tunnel or multicast channel | Individual group telegrams on the KNX medium |
| **Credential type** | Interface credentials, backbone key | Group key per group address |
| **Where configured** | Discovery page → Security tab | Project page (loaded with `.knxproj`) |
| **Required for** | Connecting to a secure gateway | Sending/receiving secure group telegrams |

The two mechanisms are independent. An installation may use KNX IP Secure for the IP connection without KNX Data Secure on the bus, or vice versa, or both.

See [KNX Data Secure](knx-data-secure.md) for how SharKNX handles telegram-level encryption.
