# How to Connect to a KNX Gateway

SharKNX connects to your KNX installation via a KNXnet/IP gateway on the local network. This guide covers discovering a gateway automatically, saving it for quick re-use, adding one manually, and connecting.

---

## Option A — Scan and Connect (Recommended for First Use)

1. Go to the **Discovery** page and open the **Discover** tab.
2. Tap the **scan FAB** (radar icon). The app sends KNXnet/IP discovery requests on the local network and lists any gateways that respond.
3. Locate your gateway in the results. Each card shows the gateway name, IP address, port, and whether KNX IP Secure is supported.
4. Tap **Select** on the gateway card to set it as the active gateway for the current session.
   - To save it for future sessions, tap **Save** on the card. Saved gateways appear in the **Config** tab and can be selected without scanning again.
5. Navigate to the **Monitor** page (or any page that needs a connection) and tap the **connect/start FAB**. SharKNX connects to the selected gateway automatically.

> **Last Selected Gateway:** The gateway you most recently used is remembered and shown at the top of the connection pop-up on the Monitor and Shark Hunt pages. This means you usually don't need to visit the Discovery page again after the first setup.

---

## Option B — Add a Gateway Manually

Use this when the gateway is on a different subnet or not discoverable via multicast (e.g. remote access over VPN).

1. Go to the **Discovery** page and open the **Config** tab.
2. Tap the **+ FAB** to open the manual gateway form.
3. Fill in the required fields:

   | Field | Description |
   |---|---|
   | **Name** | A label to identify this gateway in the list |
   | **IP address** | The gateway's IPv4 address |
   | **Port** | Default is `3671` |
   | **Use KNX IP Secure** | Enable if the gateway requires a secure tunnel |
   | **NAT mode** | Enable if connecting through a NAT router or firewall |

4. Tap **Save**. The gateway appears in the Config tab list and is immediately available for selection.
5. Tap the gateway entry to select it, then start the monitor or connect from a hunt page.

> The Config tab supports up to **50** saved gateways.

---

## Option C — Connect via Multicast (KNX IP Routing)

If your installation uses a KNX IP Router in routing mode, SharKNX can receive and send on the multicast group instead of tunnelling through a specific gateway.

1. Go to the **Discovery** page → **Discover** tab.
2. If no router with routing capability is found during a scan, the multicast section may not appear by default. Enable **Always show multicast options** in **Settings → Discover** to make it permanently visible.
3. Tap **Select** on the multicast option. No IP address or port configuration is needed — the app uses the multicast address and port configured in Settings → Discover (defaults: `224.0.23.12`, port `3671`).

---

## Connecting with KNX IP Secure

If the gateway requires KNX IP Secure, load your credentials in the **Security** tab of the Discovery page before connecting. See [Set Up KNX IP Secure](setup-knx-ip-secure.md).

---

## Troubleshooting

| Symptom | Likely cause |
|---|---|
| No gateways found after scan | Device and gateway are on different subnets, or multicast is blocked — try **Force unicast subnet scan** in Settings → Discover, or add the gateway manually |
| Connection times out | Gateway IP or port is wrong, or the gateway is busy with another client (most gateways support only one tunnel at a time) |
| Secure connection fails | Credentials not loaded, or wrong keystore — revisit the Security tab |
| Gateway found but cannot select | The gateway may require KNX IP Secure and credentials have not been loaded yet |
