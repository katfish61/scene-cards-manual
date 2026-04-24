<!--
TODO — still open for this chapter:
  1. Screenshots — the day-header import menu, a sound report badge,
     the inspector Shoot Data section expanded for a card with sound entries,
     the macOS "Import Sound Reports from Folder" open panel.
  2. RESOLVED — when detectShootDay returns nil the file is added to an
     `unmatched` array and listed by name in the summary alert at the end
     of the import. It is never silently dropped. §10.1.4 is accurate.
  3. Confirm whether iPadOS "Import Shoot Reports…" (⋯ overflow) is a
     folder picker or a multi-file picker — looks like FolderPicker
     from the code, but worth checking against the live UI.
  4. RESOLVED — camera and continuity parsers exist in the codebase
     (parseCameraReport, parseContinuitySheet, plus data models and
     inspector views) but are explicitly bypassed in the import switch
     with comments "too many formats to parse reliably — attach only".
     Both types are attach-only in the current build. §10.2 and §10.3
     have been corrected accordingly.
  5. Aaton Cantar and Zoom recorder formats are not mentioned in the
     parser code at all. Sound Devices PDF/CSV and Zaxcom Nomad are the
     only parsed formats. Add support TBD — update §10.2.1 when landed.
-->

# Chapter 10 — Shoot Reports

Scene Cards can attach shoot reports to shoot days. For sound reports,
it also parses the file and pulls per-take data directly onto each
matching card — so you can see filename, take, duration, tracks and
notes in the card's inspector without leaving the wall. After import,
cards on that day gain a sound badge to show they have been confirmed
by the sound report.

The other four report types — Camera, Continuity, Call Sheet and
Essentials — are stored inside the document and openable from the day
badge, but are not parsed in the current version.

Five report types are supported:

| Type | What Scene Cards does with it |
|---|---|
| **Sound** | Parses; extracts per-take entries onto each matching card |
| **Camera** | Attaches the file to the day — no parsing |
| **Continuity** | Attaches the file to the day — no parsing |
| **Call Sheet** | Attaches the file to the day — no parsing |
| **Essentials** | Attaches the file to the day — no parsing |

This chapter covers importing reports (via the day header and via folder
batch), the formats accepted for sound reports, the per-scene data shown
in the inspector, removing a report, and where the files live on disk.

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
For sound reports, the per-scene data is also written onto the matching
cards immediately.

> 🔒 **Permission required** — on 📐 iPadOS, the file picker prompts the
> first time you reach a location outside the app's sandbox.

### 10.1.2 🍎 macOS — Import Sound Reports from Folder

To batch-import a folder of Sound report PDFs across multiple shoot days
in one step:

1. Choose `File → Import Sound Reports from Folder…`.
2. Select the folder containing the report PDFs.
3. Click **Open**.

Scene Cards scans every PDF and CSV in the folder, auto-detects the
shoot day for each file (§10.1.4), and imports them all. A summary
alert reports how many entries were imported.

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
   `22Y10M25` = 25 Oct 2022).
3. **PDF header keyword** — `Day: 9`, `Production Day 9` near the top
   of the first page.
4. **PDF header date** — any recognisable date string matched against
   the schedule.

If none of the four strategies produces a match, the file is skipped.
Skipped files appear in the summary alert so you can attach them
manually via the day header (§10.1.1).

## 10.2 Accepted Formats

### 10.2.1 Sound reports

| Format | What is parsed |
|---|---|
| **Sound Devices PDF** | Filename, scene, take, duration, tracks, notes. Filename encodes episode and scene: e.g. `1329S142T01` = ep 13, sc 29, slate 142, take 1. |
| **Sound Devices CSV** | Same fields as PDF; columns detected by header name (`File Name`, `Scene`, `Take`, `Length`, `Notes`, `Trk1`…). Accepts UTF-8, UTF-16 and Latin-1 encodings. |
| **Zaxcom Nomad PDF** | Filename, scene, take, tracks, notes. Filename format: `{scene}T{take}`, e.g. `27T002`. |

When the PDF is image-based (scanned), Scene Cards falls back to Vision
OCR at 3× scale to extract the text. OCR results are used alongside any
native PDF text — deduplication prevents double-counting.

> ⓘ **Note** — the parser is tuned for Sound Devices and Zaxcom Nomad
> formats. Reports from other recorders (Aaton Cantar, Zoom, etc.) are
> not currently parsed — import them as attach-only via the day header
> and they will be available to open from the day badge.

### 10.2.2 Camera, Continuity, Call sheets and Essentials

These types are **attach-only** in the current version — Scene Cards
stores the file inside the package and makes it openable from the day
badge, but does not attempt to parse the content. Any PDF, folder or
supported file type can be attached.

## 10.3 Per-Scene Data in the Inspector

For sound reports, the extracted data appears directly on each matching
card. To view it, open the card's inspector (§6.1) and scroll to the
**Shoot Data** section.

The Shoot Data section is only shown when at least one sound entry
exists for that card — cards without any imported sound data show nothing.

### 10.3.1 Layout

Sound entries are grouped by shoot day. Each group is collapsible. Tap
or click the group header to expand or collapse it.

### 10.3.2 Sound entries

Each sound entry shows:

| Field | Example |
|---|---|
| Filename | `1329S142T01` |
| Reel / episode | `13` |
| Take | `1` |
| Duration | `00:00:57` |
| Tracks | `Mix L  Mix R  Boom A  Boom B` |
| Notes | `Good. Traffic noise on Boom B` |

## 10.4 Removing a Report

### 10.4.1 Remove a day's report badge

1. In Schedule mode, right-click the coloured badge in the day header.
2. Choose **Remove {type} (Day N)**.

This deletes the attachment record from the document. The file inside
the package (`Media/reports/…`) is **not** deleted.

For sound reports, the per-scene entries stored on the cards for that
day are also removed.

### 10.4.2 Re-import to update

There is no in-place edit for report entries. To update a day's data
after a re-export from the recorder, attach the new version via the day
header — Scene Cards clears the old sound data for that day and applies
the new import.

## 10.5 Scene Number Matching

Imported sound entries are matched to cards using normalised scene keys:

- Leading zeros are stripped: `017` → `17`.
- Episode prefixes are preserved for TV-style keys: `1-14A` stays
  `1-14A` and matches a card with episode 1, scene 14A.
- Sound Devices filenames encode episode and scene in the leading
  digits: `1329S…` → ep 13, sc 29.

Entries that don't match any card are stored against the report day
but not displayed anywhere — they don't cause an error.

## 10.6 Transferring Reports Between Documents

The **Import Session Data** workflow (§12) can copy shoot reports from
one Scene Cards document into another. You choose which shoot days and
which report types to bring across; both attachment records and
per-scene entries transfer together.

## 10.7 Where Report Files Live on Disk

Report files are copied into the document package at:

```
MyProduction.scenecards/
└── Media/
    └── reports/
        ├── Day_01_160921/       ← dated form (Day_NN_DDMMYY)
        │   ├── sound/
        │   │   └── Day01_SoundReport.pdf
        │   ├── camera/
        │   │   └── Camera_Day1.pdf
        │   ├── continuity/
        │   │   └── Continuity_Day1.pdf
        │   ├── callsheets/
        │   │   └── CallSheet_Day1.pdf
        │   └── essentials/
        │       └── Essentials_Day1.pdf
        └── Day_02/              ← legacy form (no date; older documents)
            └── sound/
                └── Day02_Sound.pdf
```

The day folder uses the dated form `Day_NN_DDMMYY` when the schedule
carries a date for that shoot day; otherwise it falls back to the bare
`Day_NN` form. Files that already exist at the destination are not
overwritten — re-importing a corrected report replaces the attachment
record but does not delete the old file.

> ⓘ **Note** — removing a badge from the day header deletes the
> attachment record; it does not delete the file from `Media/reports/`.
> To recover disk space, use **Show Package Contents** in Finder and
> delete from there.

## 10.8 Where to Go Next

- **Import Session Data** (copy reports to another document) — see §12.
- **Schedule mode day headers and badges** — see §9.6.
- **Document package layout** — see §4.8.
