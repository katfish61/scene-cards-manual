<!--
TODO — still open for this chapter:
  1. Screenshots — the day-header import menu, a sound report badge,
     the inspector Shoot Data section expanded for a card with entries,
     the macOS "Import Sound Reports from Folder" open panel.
  2. Confirm what happens when the folder-batch import cannot detect a
     shoot day for a file (detectShootDay returns nil) — is the file
     skipped silently, or does the user get prompted?
  3. Confirm whether iPadOS "Import Shoot Reports…" (⋯ overflow) is a
     folder picker or a multi-file picker — looks like FolderPicker
     from the code, but worth checking against the live UI.
     
     4. i do love the idea in principle of being able to parse from camera and continuity reports but at the moment its not possible we have not found a reliable way of doing it  - also i'm not sure what happens if the reports conflict which do we trust to re arrange the scenes in that day - the descriptions below however seem to imply we have done some work with camera and continuity reports  - we need to talk about this....
-->

# Chapter 10 — Shoot Reports

Scene Cards can attach shoot reports to shoot days and, for sound reports, pull the per-scene data directly onto each card and the cards on that day change and have orange badges if... and sound badges to show they have been conformed by sound report.... After
import, a card's inspector shows the takes, rolls and continuity notes
for that scene without leaving the wall.

Five report types are supported:

| Type | What Scene Cards does with it |
|---|---|
| **Sound** | Parses; extracts per-take entries onto each scene card and edits the cards within the day too|
| **Camera** | Attaches the file to the day — no parsing
| **Continuity** | Attaches the file to the day — no parsing
| **Call Sheet** | Attaches the file to the day — no parsing |
| **Essentials** | Attaches the file to the day — no parsing |

This chapter covers importing reports (via the day header and via folder
batch), the formats accepted for parsed types, the per-scene data shown
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
For the sound...., the per-scene data is also written onto the
matching cards immediately.

> 🔒 **Permission required** — on 📐 iPadOS, the file picker prompts the
> first time you reach a location outside the app's sandbox.

### 10.1.2 🍎 macOS — Import Sound Reports from Folder

To batch-import a folder of Sound report PDFs across multiple shoot days
in one step:

1. Choose `File → Import Sound Reports from Folder…`.
2. Select the folder containing the report PDFs.
3. Click **Open**.

Scene Cards scans every PDF and CSV in the folder, auto-detects the
shoot day for each file (§10.1.3), and imports them all. A summary
alert reports how many entries were imported.

> ✱ **Tip** — name your Sound Devices exports to include the shoot day
> (e.g. `Day_09_soundreport.pdf` or `Day9_22Y10M25_1.pdf`). The
> detector reads both the `Day N` pattern and Sound Devices date
> encoding (`YYYYYMMdd`) and matches them against the imported schedule.

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

***we need to look at aaton cantar reports and also zoom reports

When the PDF is image-based (scanned), Scene Cards falls back to Vision
OCR at 3× scale to extract the text. OCR results are used alongside any
native PDF text — deduplication prevents double-counting.

> ⓘ **Note** — the parser is tuned for Sound Devices and Zaxcom Nomad
> formats. Reports from other recorders may import fewer entries or none
> at all if the layout doesn't match.

### 10.2.2 Camera reports  **I'm not sure this is true check it and let me know

Scene Cards parses **VES / Movie Slate** format PDFs. The parser looks
for scene header rows (`Scene: 17A`, `Sc. 17`, etc.) followed by
roll/take rows (`A001  3  …`). Fields extracted per take: roll, take
number, filter, shutter angle, T-stop, fps, lens serial, focal length,
height, tilt, focus distance and notes.

Other camera report formats are not currently parsed — attach the PDF
via the day header (type: Camera) and it will be available to open from
the day badge.

### 10.2.3 Continuity sheets
 **I'm not sure this is true check it and let me know
The continuity parser handles a standard shot-list layout: each row
begins with a scene number, followed by take number, an optional
**P** (printed) or **NG** flag, an optional screen time, and a
description. Both film-style (`17`) and TV-style (`1-17`) scene
numbers are accepted.

### 10.2.4 Call sheets and Essentials

These types are **attach-only** — Scene Cards stores the file inside
the package and makes it openable from the day badge, but does not
attempt to parse the content. Any  **folders too** PDF or supported file can be attached.

## 10.3 Per-Scene Data in the Inspector

For the sound report , the extracted data appears directly
on each matching card. To view it, open the card's inspector (§6.1)
and scroll to the **Shoot Data** section.

The Shoot Data section is only shown when at least one sound, camera
or continuity entry exists for that card — cards without any imported
data show nothing.

### 10.3.1 Layout

Entries are grouped by report type and then by shoot day. Each group
is collapsible. Tap or click the group header to expand or collapse it.

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

### 10.3.3 Camera entries

Each camera entry shows:

| Field | Example |
|---|---|
| Roll | `A012` |
| Take | `3` |
| Filter | `ND 0.6` |
| Shutter | `172.8°` |
| T-stop | `T2.8` |
| FPS | `23.976` |
| Lens serial | `41523` |
| Focal length | `32mm` |
| Height | `Low` |
| Tilt | `Level` |
| Focus distance | `2.4m` |
| Notes | `Slight focus pull on action` |

### 10.3.4 Continuity entries

Each continuity entry shows:

| Field | Example |
|---|---|
| Take | `3` |
| Circled / printed | `P` (printed) or `NG` |
| Screen time | `0:42` |
| Description | `SAMIR walks in, sits. Hair left.` |

## 10.4 Removing a Report

### 10.4.1 Remove a day's report badge

1. In Schedule mode, right-click the coloured badge in the day header.
2. Choose **Remove {type} (Day N)**.

This deletes the attachment record from the document. The file inside
the package (`Media/reports/…`) is **not** deleted.

For the three parsed types (Sound, Camera, Continuity), the per-scene
entries stored on the tiles for that day are also removed.

### 10.4.2 Re-import to update

There is no in-place edit for report entries. To update a day's data
after a re-export from the recorder or editing app, attach the new
version via the day header — Scene Cards clears the old data for that
day and type, then applies the new import.

## 10.5 Scene Number Matching

Imported entries are matched to cards using normalised scene keys:

- Leading zeros are stripped: `017` → `17`.
- Episode prefixes are preserved for TV-style keys: `1-14A` stays
  `1-14A` and matches a card with episode 1, scene 14A.
- Sound Devices filenames encode episode and scene in the leading
  digits: `1329S…` → ep 13, sc 29.

Entries that don't match any card are stored against the report day
but not displayed anywhere in the current build — they don't cause an
error.

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
