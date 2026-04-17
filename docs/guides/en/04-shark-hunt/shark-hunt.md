# Shark Hunt

**Shark Hunt** lets you build custom action pages for quick KNX control and diagnostics. Each hunt is a collection of actions - send commands and bus monitors - that can be executed with a single tap. Hunts can be created directly in the app, exported as files, and shared with colleagues or clients, so they can import and run them independently for remote troubleshooting or handover scenarios.

A hunt can contain two types of actions:
- **Send Actions** - send fixed commands, sequences of commands, or variable commands to the KNX bus
- **Monitor Actions** - monitor the bus with custom filters, scoped to a specific space or a specific device

This guide covers all pages and options available in Shark Hunt in detail.

> [!NOTE]
> Shark Hunts are stored as `.json` files with a defined structure. If you want to create or edit hunts manually outside the app, see the [Shark Hunt Advanced Topics](advanced-topics.md) guide.

---

## Contents

- [Shark Hunts Page](#shark-hunts-page)
  - [Top Bar](#top-bar)
  - [Filter Bar](#filter-bar)
  - [Hunt Cards](#hunt-cards)
  - [Multi-Select](#multi-select)
  - [Menu Panel](#menu-panel)
- [Hunt Page](#hunt-page)
  - [Top Bar](#top-bar-1)
  - [Badges](#badges)
    - [Hunt Info Badge](#hunt-info-badge)
    - [Connection Badge](#connection-badge)
    - [ETS Project Badge](#ets-project-badge)
    - [Data Secure Badge](#data-secure-badge)
    - [Gateway Badge](#gateway-badge)
  - [Connecting to the Bus](#connecting-to-the-bus)
  - [Action Cards](#action-cards)
- [Hunt Monitor Page](#hunt-monitor-page)

---

## Shark Hunts Page

The **Shark Hunts Page** is the main entry point for Shark Hunt. It lists all your created hunts as cards and provides options to search, import, and manage them.

<div align="center">

  | Shark Hunts Page |
  |------------------|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-main-page.png" alt="Shark Hunts Main Page" width="400" /> |

</div>

### Top Bar

The top bar contains two buttons on the right side:

| Button | Description |
|--------|-------------|
| **Import** | Import a `.json` hunt file from your device. You can import a file containing a single hunt or multiple hunts at once. If an imported hunt has the same name as an existing one, it is added as a copy with the same name |
| **Help (?)** | Opens the help page with additional information about Shark Hunt |

<div align="center">

  | Shark Hunt Help Page |
  |----------------------|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-main-page-help.png" alt="Shark Hunt Help Page" width="400" /> |

</div>

### Filter Bar

Below the top bar, a filter row allows you to search through your hunts by name or description. A **star icon button** next to the search input lets you quickly toggle a view showing only your favorited hunts.

### Hunt Cards

Each hunt is displayed as a card. The card **border color** indicates the hunt type at a glance:

| Color | Hunt Type |
|-------|-----------|
| 🟢 Green | Commands only |
| 🔵 Blue | Monitor only |
| 🔴 Red | Combined (send + monitor) |

Each card shows:
- **Name** and **Description** of the hunt
- **Type** label (Commands, Monitor, or Combined)
- **Number of actions** (e.g. *2 actions*)
- **Star icon** — tap to mark/unmark the hunt as a favorite
- **3-dot menu** — opens a menu with the following options:

| Option | Description |
|--------|-------------|
| **Edit** | Open the hunt editor to modify it |
| **Export** | Export this hunt as a `.json` file |
| **Share** | Share the hunt file via your device's share sheet |
| **Delete** | Delete this hunt |
| **Info** | Opens a bottom sheet with full hunt details: basic info, full list of actions, creation date and last modified date |

Tapping the card itself navigates to the [Hunt Page](#hunt-page) for that hunt.

> [!NOTE]
> You can have a maximum of **25 hunts** in the app.

---

### Multi-Select

Long-pressing a hunt card enters **multi-select mode**. You can then tap additional cards to add them to the selection. While in multi-select mode, the top bar shows three action buttons:

| Button | Description |
|--------|-------------|
| **Copy** | Creates a copy of each selected hunt |
| **Export** | Exports the selected hunts together into a single `.json` file |
| **Delete** | Deletes all selected hunts |

<div align="center">

  | Shark Hunt Multi-Select |
  |-------------------------|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-main-page-multiple-select.png" alt="Shark Hunt Multi-Select" width="400" /> |

</div>

---

### Menu Panel

The **hamburger icon** (top-left) opens a side panel with a summary of all your hunts and bulk management options.

<div align="center">

  | Shark Hunt Menu Panel |
  |-----------------------|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-main-page-menu.png" alt="Shark Hunt Menu Panel" width="400" /> |

</div>

The summary card shows:

| Stat | Description |
|------|-------------|
| **Total Hunts** | Total number of hunts in the app |
| **Favorites** | Number of hunts marked as favorite |
| **Commands** | Hunts that contain only send actions |
| **Monitor** | Hunts that contain only monitor actions |
| **Combined** | Hunts that contain both send and monitor actions |

Below the summary, two action buttons are available:

| Button | Description |
|--------|-------------|
| **Import** | Import a `.json` file — same as the top bar import button |
| **Export All** | Exports all your hunts together into a single `.json` file |

> [!WARNING]
> The **Delete All** button at the bottom of the panel permanently removes all hunts from the app. This action cannot be undone.

---

## Hunt Page

Tapping a hunt card on the [Shark Hunts Page](#shark-hunts-page) opens the **Hunt Page** for that hunt. This is where you execute actions - send commands to the KNX bus or launch a bus monitor - with a single tap.

<div align="center">

  | Hunt Page |
  |-----------|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-action-page-overview.png" alt="Hunt Page" width="400" /> |

</div>

### Top Bar

The top bar contains a **back button** on the left to return to the Shark Hunts Page, and a **filter input** on the right to search through the actions in the current hunt by name.

---

### Badges

Below the top bar, a row of floating badges provides quick access to context and controls for the current hunt session.

---

#### Hunt Info Badge

Displays the **name of the current hunt**. Tapping it opens a bottom sheet with the hunt's full details — the same information shown in the **Info** option on the Shark Hunts Page.

<div align="center">

  | Hunt Info Badge |
  |-----------------|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-badge-info.png" alt="Hunt Info Badge" width="400" /> |

</div>

---

#### Connection Badge

Displays the current **connection status** — either connected or disconnected. Tapping it triggers a connect or disconnect to the selected gateway.

> [!NOTE]
> See [Connecting to the Bus](#connecting-to-the-bus) for details on how gateway selection works.

---

#### ETS Project Badge

Indicates whether an **ETS project** is currently loaded. The badge is **green** when a project is loaded and **red** when none is loaded.

Tapping it opens a bottom sheet:

- **If a project is loaded** — shows the project details and an **Unload Project** button
- **If no project is loaded** — shows a **Load Project** button, which triggers the same project load flow described in the [ETS Project Explorer](../../03-ets-project-explorer.md) guide

<div align="center">

  | ETS Project Badge — Loaded | ETS Project Badge — No Project |
  |:--------------------------:|:------------------------------:|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-badge-ets-loaded.png" alt="ETS Badge Loaded" width="400" /> | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-badge-ets-empty.png" alt="ETS Badge No Project" width="400" /> |

</div>

---

#### Data Secure Badge

Indicates whether **KNX Data Secure senders** are configured for this session.

- **Gray** — no Data Secure senders configured
- **Green** — Data Secure senders are configured

Tapping it opens a bottom sheet:

- **If no project is loaded** — shows an informational message only
- **If a project is loaded and senders are configured** — shows the configured sender details and a **Configure Senders** button, which navigates to the same secure sender configuration page described in the [ETS Project Explorer](../../03-ets-project-explorer.md) guide

<div align="center">

  | Data Secure Badge — Configured | Data Secure Badge — Not Configured |
  |:------------------------------:|:-----------------------------------:|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-badge-secure-configured.png" alt="Data Secure Badge Configured" width="400" /> | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-badge-secure-empty.png" alt="Data Secure Badge Not Configured" width="400" /> |

</div>

---

#### Gateway Badge

Displays the **IP address of the selected gateway**, or *"No Gateway Selected"* if none has been chosen yet.

- **If a gateway is selected** — tapping opens a bottom sheet with the gateway details and a **Clear Gateway** button to deselect it
- **If no gateway is selected** — the badge is not tappable

<div align="center">

  | Gateway Badge |
  |---------------|
  | <img src="../../../../assets/screenshots/shark-hunts/shark-hunt-badge-gateway.png" alt="Gateway Badge" width="400" /> |

</div>

---
