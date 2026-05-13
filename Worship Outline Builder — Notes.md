# Worship Outline Builder — Project Notes
**Saint Paul's United Church of Christ**
*Last updated: May 13, 2026*

---

## What this is

A single-file web app (`index.html`) that turns a Google Doc worship outline into a formatted, printable bulletin. No installation required — runs in any browser.

The current version is hosted on GitHub Pages. The file in this folder is your local backup copy.

---

## Weekly workflow

1. Finalize the order of service in Google Docs as usual.
2. Open the Bulletin Builder in your browser (GitHub Pages URL).
3. Click **📄 From Google Doc** and paste the Google Doc text into the dialog.
4. The app parses the text automatically into structured service items.
5. Review and adjust anything in the editor panel on the left.
6. Click **🖨 Print / PDF** to save a PDF or send to the printer.

---

## Action bar buttons

| Button | What it does |
|---|---|
| 🗒 New Week | Clears everything and resets to the blank default order of service |
| 📄 From Google Doc | Paste your Google Doc outline text — auto-parses into service items |
| ⬆ Import JSON | Load a previously saved bulletin back into the editor |
| ⬇ Save JSON | Save the current bulletin as a .json file for reuse or backup |
| 🖨 Print / PDF | Opens the browser print dialog — choose "Save as PDF" |

---

## Google Doc import rules

- **Date, time, liturgical Sunday** are read from the first two lines automatically.
- **ALL CAPS lines** (WE GATHER, WE SHARE THE WORD, etc.) become section dividers.
- **Label: Detail** lines become service items.
- **Scripture Readings** groups sub-readings underneath it: Gospel, Old Testament, Epistle, Prayer of Illumination, any Bible reference (Book Chapter:Verse), etc.
- **Scripture Response** stays as its own standalone item (it's congregational singing).
- **Holy Communion** becomes its own section header. The comma-separated list on the next line (Invitation, Words of Institution, etc.) expands into individual items. Communion Song and Communion Servers follow as normal items.
- **On communion Sundays**, a PRAYER section header is automatically inserted before Prayers of the People.
- **On non-communion Sundays**, Prayers of the People stays inside the WE RESPOND WITH THANKSGIVING section.
- **The Lord's Prayer** is always its own item (curly apostrophes from Google Docs are handled automatically).

---

## Icons used

| Icon | Used for |
|---|---|
| ⚬ | Spoken/liturgical items (welcome, prayer, sermon, etc.) |
| 🎼 | Congregational singing (hymns, kyrie, doxology, etc.) |
| 🎵 | Instrumental/choral music (prelude, postlude, offering of music) |

---

## Saved Bulletins folder

The `Saved Bulletins` subfolder contains `.json` snapshots of past services. Load any of them with **⬆ Import JSON** to reuse or reference.

---

## Files in this folder

| File | Purpose |
|---|---|
| `index.html` | The app itself — open in any browser |
| `Worship-Outline-Builder-Quickstart.docx` | One-page quick reference for weekly use |
| `Worship-Outline-Builder-Team-Cheatsheet.docx` | Cheatsheet for staff/volunteers |
| `Saved Bulletins/` | JSON snapshots of past services |

---

## Technical notes (for future Claude sessions)

- Single-file HTML/CSS/JS app — everything is in `index.html`.
- The live version is on GitHub Pages. Push `index.html` to the repo to update it.
- `svcOrder` is the master data array — both the default template and the live working data.
- `render()` builds the bulletin preview from `svcOrder`.
- `buildOrderUI()` builds the editor panel from `svcOrder` — called at startup and after import/clear.
- `gdocParse()` handles all Google Doc text parsing.
- Print/PDF only works when served from GitHub Pages or a web server (not from a local file:// path in Chrome).
