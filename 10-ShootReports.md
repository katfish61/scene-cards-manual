<!--
TODO — still open for this chapter:
  1. Screenshots still needed: the day-header import menu, a sound report
     badge on the day header, the macOS "Import Sound Reports from Folder"
     open panel; the inspector Reports section showing open buttons.
  2. Confirm whether iPadOS "Import Shoot Reports…" (⋯ overflow) is a
     folder picker or a multi-file picker — looks like FolderPicker
     from the code, but worth checking against the live UI.
-->

# Chapter 10 — Shoot Reports

Scene Cards can attach shoot reports to shoot days and store them inside
the document package. After import, each report file is one tap away
from the card inspector — click to open it in Preview or your default
PDF viewer. Cards on that day gain a colour-coded badge in the schedule
header.

Five report types are supported:

| Type | What Scene Cards does with it |
|---|---|
| **Sound** | Stores the file; parses scene keys to schedule cards to the shoot day; opens the whole PDF from the inspector |
| **Camera** | Stores the file; opens from the day badge |
| **Continuity** | Stores the source PDF; also extracts per-scene pages into the reference carousel; opens from the inspector |
| **Call Sheet** | Stores the file; opens from the day badge |
| **Essentials** | Stores the file; opens from the day badge |

This chapter covers importing reports (via the day header and via folder
batch), the formats accepted for sound reports, the inspector Reports
section, removing a report, and where the files live on disk.

## 10.1 Attaching a Report to a Shoot Day

Reports are attached at the shoot-day level. You must have a schedule
imported first (§9) so the day structure exists.

### 10.1.1 From the day header

1. In Schedule mode, locate the shoot day.
2. Click the **↓doc** button at the right of the day header.
3. From the menu, choose a report type:
   **Sound**, **Camera**, **Continuity**, **Call Sheet** or **Essentials**.
4. In the file picker, select the report file (or folder — see below).

For **Camera**, **Continuity**, **Call Sheet** and **Essentials** on
🍎 macOS, the open panel also accepts **folders** — single-click a
folder, then click **Open** to import everything inside it as a batch
for that day and type. For **Sound**, use the folder-batch route
(§10.1.2) to get automatic day detection across multiple days.

After import, a colour-coded badge appears in the day header (§9.6).
Sound reports also reschedule any matching cards to that shoot day.

> 🔒 **Permission required** — on 📐 iPadOS, the file picker prompts the
> first time you reach a location outside the app's sandbox.

### 10.1.2 🍎 macOS — Import Sound Reports from Folder

To batch-import a folder of Sound report PDFs across multiple shoot days
in one step:

1. Choose `File → Import Sound Reports from Folder…`.
2. Select the folder containing the report PDFs.
3. Click **Open**.
4. Enter the shoot day number that corresponds to the earliest date in
   the folder (e.g. `46` for shoot day 46).

Scene Cards scans every PDF and CSV in the folder, auto-detects the
shoot day for each file (§10.1.4), and imports them all. A summary
alert reports how many days were imported.

> ✱ **Tip** — name your Sound Devices exports to include the shoot day
> (e.g. `Day_09_soundreport.pdf` or `Day9_22Y10M25_1.pdf`). The
> detector reads both the `Day N` pattern and Sound Devices date
> encoding (`YYYYMMdd`) and matches them against the imported schedule.

### 10.1.3 📐 iPadOS — Import Shoot Reports

Tap **⋯** → **Import Shoot Reports…** to open a folder picker. Navigate
to the folder of reports and confirm. Scene Cards applies the same
day-detection logic as the macOS folder batch.

### 10.1.4 Shoot day auto-detection

When a report is imported via a folder (not via the day header), Scene
Cards tries to identify its shoot day using four strategies in order:

1. **Filename day pattern** — `Day_09`, `Day-9`, `day 9`, `D09` etc.
2. **Filename date** — parsed and matched against the imported schedule.
   Sound Devices devices encode the date as `YYYYMMdd` (e.g.
   `22Y10M25` = 25 Oct 2022). Aaton Cantar encodes it as `MM-DD-YY`
   at the end of the filename.
3. **PDF header keyword** — `Day: 9`, `Production Day 9` near the top
   of the first page.
4. **PDF header date** — any recognisable date string matched against
   the schedule.

If none of the four strategies produces a match, the file is skipped.
Skipped files appear in the summary alert so you can attach them
manually via the day header (§10.1.1).

## 10.2 Accepted Formats

### 10.2.1 Sound reports

Sound report files are stored in the document package and opened
directly — Scene Cards reads the scene keys to schedule the matching
cards to the correct shoot day but does not store individual take data.

| Recorder | Detection |
|---|---|
| **Sound Devices** (PDF or CSV) | Filename encodes episode and scene: e.g. `1329S142T01` = ep 13, sc 29. |
| **Zaxcom Nomad** (PDF) | Filename format `{scene}T{take}`, e.g. `27T002`. |
| **Aaton Cantar** (PDF) | `Slt` column contains the scene reference; date detected from `MM-DD-YY` filename suffix. |

When the PDF is image-based (scanned), Scene Cards falls back to Vision
OCR at 3× scale to extract the text.

### 10.2.2 Camera, Continuity, Call sheets and Essentials

These types are **attach-only** — Scene Cards stores the file inside the
package and makes it openable from the inspector or day badge. Any PDF,
folder or supported file type can be attached.

Continuity PDFs are a special case: Scene Cards also parses each page
for its scene number and places those pages into the matching card's
reference carousel (§6.4), so you can flip through the continuity sheets
directly on the card. The matched cards are scheduled to the shoot day
you specify at import. The full source PDF is archived in
`Media/reports/` at the same time (§10.7).

## 10.3 Opening Reports from the Inspector

After import, a **Reports** section appears at the bottom of the card
inspector for any card that has sound reports for its shoot day, or
camera and continuity entries.

Each sound report appears as a row showing the report type, shoot day
and filename. Click or tap the row to open the full PDF in your default
viewer (Preview on macOS).

The Reports section is only shown when at least one report is associated
with the card.

## 10.4 Removing a Report

### 10.4.1 Remove a day's report badge

1. In Schedule mode, right-click the coloured badge in the day header.
2. Choose **Remove {type} (Day N)**.

This deletes the attachment record from the document. The file inside
the package (`Media/reports/…`) is **not** deleted.

### 10.4.2 Re-import to update

There is no in-place edit. To update after a re-export from the
recorder, attach the new version via the day header — Scene Cards clears
the old attachment record and replaces it with the new file.

## 10.5 Scene Number Matching

Sound scene keys are normalised before matching cards:

- Leading zeros are stripped: `017` → `17`.
- Episode prefixes are preserved for TV-style keys: `1-14A` stays
  `1-14A` and matches a card with episode 1, scene 14A.
- Sound Devices filenames encode episode and scene in the leading
  digits: `1329S…` → ep 13, sc 29.
- Setup letters (American slating: `7A`, `7B`) are matched both as-is
  and against the bare scene number, so they find whichever convention
  the cards use.

## 10.6 Transferring Reports Between Documents

The **Import Session Data** workflow (§12) can copy shoot reports from
one Scene Cards document into another. You choose which shoot days and
which report types to bring across; attachment records transfer together.

## 10.7 Where Report Files Live on Disk

All report files are copied into the document package at import time:

```
MyProduction.scenecards/
└── Media/
    └── reports/
        ├── Day_01_160921/       ← dated form (Day_NN_DDMMYY)
        │   ├── sound/
        │   │   └── Day01_SoundReport.pdf
        │   ├── camera/
        │   │   └── Camera_Day1.pdf
        │   ├── callsheets/
        │   │   └── CallSheet_Day1.pdf
        │   └── essentials/
        │       └── Essentials_Day1.pdf
        ├── Day_02/              ← legacy form (no date; older documents)
        │   └── sound/
        │       └── Day02_Sound.pdf
        └── Day_46_160521/       ← continuity source PDFs filed under the shoot day
            └── continuity/
                └── ContinuityLog.pdf
```

The day folder uses the dated form `Day_NN_DDMMYY` when the schedule
carries a date for that shoot day; otherwise it falls back to the bare
`Day_NN` form.

Files that already exist at the destination are not overwritten —
re-importing a corrected report replaces the attachment record but does
not delete the old file.

> ⓘ **Note** — removing a badge from the day header deletes the
> attachment record; it does not delete the file from `Media/reports/`.
> To recover disk space, use **Show Package Contents** in Finder and
> delete from there.

## 10.8 Where to Go Next

- **Import Session Data** (copy reports to another document) — see §12.
- **Schedule mode day headers and badges** — see §9.6.
- **Document package layout** — see §4.8.
