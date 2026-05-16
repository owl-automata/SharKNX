# KNX Data Secure

KNX Data Secure is the application-layer security extension to the KNX standard. It encrypts and authenticates individual KNX telegrams on the bus medium (TP or RF), protecting them from interception and manipulation regardless of how they are transported to the IP network.

> This page explains what KNX Data Secure is and how SharKNX handles it. For the step-by-step setup procedure, see [Set Up KNX Data Secure](../how-to/setup-knx-data-secure.md).

---

## What KNX Data Secure Protects

Standard KNX telegrams transmitted over twisted pair are readable by any device on the same bus segment. KNX Data Secure addresses this by encrypting the application data of selected group telegrams using **AES-128 CCM**, the same cipher used by KNX IP Secure. Each encrypted telegram also carries a **Message Authentication Code (MAC)** and an incrementing **sequence number**, which together prevent:

- Eavesdropping — the telegram payload cannot be read without the group key
- Tampering — any modification to the payload invalidates the MAC
- Replay attacks — a captured telegram cannot be replayed because its sequence number would be out of order

KNX Data Secure operates at the KNX application layer, inside the telegram itself. It is independent of the transport path — a data secure telegram is just as protected whether it travels over TP, RF, or a KNXnet/IP tunnel.

---

## Group Keys and the Sender List

Each KNX Data Secure group address has its own **group key**. The key is used to both encrypt the payload and compute the MAC. It is stored in the ETS project keyring and distributed to all devices connected to that group address during commissioning.

In addition to encryption, KNX Data Secure devices maintain a **trusted sender list** per group address: a set of individual addresses whose telegrams the device will accept. Telegrams arriving from an individual address not on this list are silently discarded, even if the encryption is correct. This means:

- To **receive** data secure telegrams correctly, you need the group key.
- To **send** data secure commands that a device will act on, your individual address must be on the device's trusted sender list for that group address.

---

## Receiving Data Secure Telegrams in SharKNX

SharKNX extracts all data secure group keys automatically when you load a `.knxproj` file. No separate credential setup is required for monitoring. Once a project is loaded:

- Incoming data secure telegrams in the Monitor are transparently decrypted and shown with their decoded value, name, and datapoint type — exactly like non-secure telegrams.
- If no project is loaded, data secure telegrams appear as raw hex with no decoded value (the payload is encrypted and unreadable without the key).

The **Data Secure badge** in the Monitor page badge row reflects the current state: grayed out if no data secure group addresses are present in the loaded project, amber if data secure addresses are loaded but senders have not been configured, and green when senders are configured and sending is ready.

<img src="../../../../assets/screenshots/guides/concepts/knx-data-secure/knx-data-secure-project-banner.png" width="320" alt="Project page with the data secure banner prompting sender configuration after loading a project with data secure group addresses" />

---

## Sending Data Secure Telegrams — the Sender Address

When SharKNX sends a data secure command, it must present an individual address that the target device recognises as a trusted sender. If the address is not on the device's sender list, the command is ignored.

SharKNX handles this through the **Data Secure Senders** configuration, accessible from the banner that appears in the Project page when a project with data secure group addresses is loaded.

In the senders page you can:

- Set a **global sender address** — used for any data secure group address that does not have a specific address configured.
- Set **per-address overrides** — map individual group addresses to specific sender individual addresses.
- **Auto-generate from project data** — SharKNX reads the ETS project and automatically creates the group address ↔ individual address mappings based on which devices are connected to each secure group address. This is the fastest way to set up senders when you have a complete project.

<img src="../../../../assets/screenshots/guides/concepts/knx-data-secure/knx-data-secure-senders.png" width="320" alt="Data Secure Senders configuration page showing global sender and per-address mapping list" />

---

## The Sender Address Constraint with KNX IP Secure

When SharKNX is connected via a **KNX IP Secure tunnel**, the individual address used in all outgoing telegrams is fixed by the gateway to the address of the tunneling connection interface. SharKNX cannot override this address — it is a property of the KNX IP Secure protocol.

This creates a practical constraint: for a data secure device to accept commands from SharKNX over a KNX IP Secure tunnel, the tunneling interface address must already be on the device's trusted sender list in ETS.

Two approaches work well in practice:

1. **Use a dedicated dummy interface in ETS.** Create a virtual secure interface device in your ETS project and connect all data secure group addresses to it. Assign its individual address as the sender in SharKNX. This keeps SharKNX's access cleanly separated from other clients.

2. **Connect data secure group addresses to the gateway's tunneling interface.** In ETS, associate the data secure group addresses with the tunneling connection interface of your KNX IP Secure gateway. Any client connecting through that interface (including SharKNX) will then be recognised as a trusted sender by the field devices.

> If you are connecting without KNX IP Secure (standard unencrypted tunnel), SharKNX can use any individual address you configure as the sender, and this constraint does not apply.

---

## Tool Keys for Device Management

KNX Data Secure also applies to device management operations — reading device info, toggling programming mode, resetting a device, programming an individual address, or reading communication tables. Devices that require tool-level authentication will reject management commands from unknown sources.

When you load a `.knxkeys` file in the **Security tab** of the Discovery page, SharKNX automatically extracts any **tool keys** present in the file and stores them. These keys enable encrypted device management communication with the corresponding Data Secure devices — no additional configuration is needed once the keys are loaded.

Tool keys are separate from the group keys embedded in the `.knxproj` file. If your installation uses Data Secure device management, you need the `.knxkeys` file (or the `.knxproj` file, which also contains tool keys) loaded in the Security tab, in addition to the project loaded in the Project page.

---

## Further Reading

For a detailed technical explanation of the KNX Data Secure protocol, the ABB "i-bus KNX Data Secure" application note is a thorough resource covering the cryptographic mechanisms, sequence number management, and ETS configuration in depth.

---

## KNX Data Secure vs. KNX IP Secure

| | KNX Data Secure | KNX IP Secure |
|---|---|---|
| **Scope** | KNX telegram (application layer) | IP transport layer |
| **What it encrypts** | Individual group telegrams on the KNX medium | The UDP/TCP tunnel or multicast channel |
| **Credential type** | Group key per group address; tool keys per device | Interface credentials; backbone key |
| **Where configured in SharKNX** | Project page (keys from `.knxproj`); Security tab (tool keys) | Discovery page → Security tab |
| **Required for** | Sending/receiving secure group telegrams | Connecting to a KNX IP Secure gateway |

The two mechanisms are independent and can be used separately or together. See [KNX IP Secure](knx-ip-secure.md) for the transport-layer counterpart.
