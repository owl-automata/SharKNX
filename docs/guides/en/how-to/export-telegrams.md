# How to Export Telegrams

SharKNX can export the telegrams currently in the monitor list to a file. You can choose the columns to include, the number of telegrams, column header style, and delimiter format. Exported files can be saved locally or shared directly from the app.

---

## From the Monitor Page

1. Start a monitor session and let telegrams accumulate, or stop the monitor when you have the traffic you need.
2. Tap the **export icon** (top right of the filter bar row) to open the export sheet.
3. Configure the export:

   | Option | Description |
   |---|---|
   | **File name** | Pre-filled with a timestamp. Edit to give the file a meaningful name. |
   | **Columns** | Tick the columns to include: ID, Time, Source, Destination, Name\*, Type, Value\*, Raw (\*requires a loaded ETS project) |
   | **Number of telegrams** | How many telegrams to export (counted from most recent). Use this to limit a large buffer to the last N entries. |
   | **Include column headers** | Toggle on to include a header row at the top of the CSV. |
   | **Delimiter** | Comma (default), Tab, or Semicolon. |

4. Tap **Save** to save the file to your device, or **Share** to open the system share sheet and send it directly to email, cloud drive, or another app.

---

## From the Shark Hunt Monitor

The same export sheet is available inside a Shark Hunt monitor session. Tap the **save/export button** in the top bar (active when telegrams are present). All the same options apply.

---

## Notes

- **Name** and **Value** columns are only meaningful when an ETS project is loaded. Without a project, those columns will be empty for most telegrams.
- **Raw** is always available and contains the unparsed hex payload — this is the ground truth value that the app parses into a human-readable value when a project is loaded.
- The export captures whatever is currently in the telegram buffer. If the buffer has reached its limit (default 2000, configurable in **Settings → Monitor**), older telegrams have already been overwritten. Export before the buffer fills if you need a long capture.
- Exported files can be re-imported into the monitor for review. From the **Monitor → tune menu**, use **Import CSV** to load a previously exported file back into the telegram list.
