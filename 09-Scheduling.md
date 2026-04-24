<!--
TODO — still open for this chapter:
  1. Screenshots — Schedule mode empty state, a populated day section
     with a full card and a placeholder, the selection bar, the
     day-header report badges, the context menu on a card.
  2. RESOLVED — iPadOS has exactly two one-liner import entry points:
     (a) the empty-state "Import One-Liner PDF" button, and
     (b) the "Re-import" button in the schedule top bar.
     The IOSNavToolbar overflow (⋯) menu has NO one-liner option —
     only script import, images, photos, shoot reports, and print.
     §9.2.1 and §9.2.2 are accurate as written.
  3. RESOLVED — a scene that appears in two shoot days in the one-liner
     renders as a full card in BOTH days (tileGrid runs matchedTile
     independently per day; no deduplication guard). This is the
     intended behaviour for scenes split across multiple shoot days.
     The second occurrence is not a placeholder and not silently dropped.
     The Unmatched section correctly excludes it. Shift-select
     deduplicates via orderedTileIDs so the tile counts once in a range.
     §9.4.2 and §9.8 have been updated to document this.
-->

# Chapter 9 — Scheduling

**Schedule mode** reorganises the wall into shoot days drawn from an
imported one-liner PDF. Instead of script order, you see each day's
scenes as a grid of cards — with crew call, total pages and report
badges in the day header. Call sheets, sound, camera and continuity
reports can all be attached per day (§9.6), and a tidy **Unmatched**
section at the bottom catches any cards not yet accounted for.

This chapter covers switching into Schedule mode, importing and
re-importing the one-liner, how cards are matched to schedule entries,
moving cards between days, multi-select, and what the various badge
colours mean. Attaching sound, camera and continuity reports to a day
is in §10.

## 9.1 Switching to Schedule Mode

Three routes reach Schedule mode:

| Route | Action |
|---|---|
| Toolbar | Tap or click the **Schedule** segment |
| Keyboard | `⌘⇧3` |
| Menu | `View → Schedule` |

`⌘⇧1` and `⌘⇧2` return to **Scenes** and **Locations** respectively.

Without an imported one-liner, Schedule mode shows an empty state with
a single **Import One-Liner PDF** button. Once a schedule is loaded,
the full day-by-day view appears.

## 9.2 Importing a One-Liner

The one-liner is the shoot schedule — a PDF strip board that lists
scenes grouped by shoot day, with crew call times and page counts.
Scene Cards reads the PDF and builds the day structure automatically.

### 9.2.1 First import

1. Switch to Schedule mode.
2. Tap or click **Import One-Liner PDF** in the centre of the screen.
3. Select the PDF from the file picker and click **Open**.

Scene Cards parses the PDF, matches each scene number against the cards
on your wall, and populates the schedule. A progress indicator appears
while parsing runs.

### 9.2.2 Re-import

To update the schedule when a new one-liner is issued, click
**Re-import** in the top bar. The existing schedule is replaced
entirely. Manual day assignments you have made (§9.5) are preserved
unless the affected scene no longer appears in the new PDF.

> ⚠ **Caution** — re-importing replaces the full schedule. Any manual
> "Remove from Schedule" edits you made to individual scenes are lost.
> Manual day assignments (the orange-badge overrides) survive.

### 9.2.3 OCR warning

When the one-liner is a scanned image PDF rather than a text PDF, Scene
Cards falls back to OCR to extract the scene numbers. An orange
**OCR — verify scene numbers** badge appears in the top bar. Check the
Unmatched section (§9.4.3) after import and manually assign any cards
that landed incorrectly.

## 9.3 The Schedule Top Bar

When a schedule is loaded, a persistent bar appears at the top of
Schedule mode showing:

- **Source filename** — the name of the imported PDF.
- **Day / scene / match counts** — e.g. `12 shoot days · 87 scenes · 84 matched`.
- **OCR badge** — orange, when OCR was used (§9.2.3).
- **Re-import** button — replaces the current schedule.

## 9.4 Reading the Day View

### 9.4.1 Day header

Each shoot day opens with an indigo **DAY N** badge plus the date (if
the one-liner carried one). To the right:

| Element | Meaning |
|---|---|
| 🕐 Crew call | Start–end times from the one-liner |
| 🗒 Total pages | Page count for the day |
| ⚠ N unmatched | Scenes in the one-liner with no matching card |
| Report badges | Colour-coded icons for attached reports (§9.6) |
| ↓doc button | Opens the **Attach Report** menu for this day (§10) |

### 9.4.2 Scene cards

Cards that matched a schedule entry appear as full tiles — still image
(if one has been attached), scene number, description and synopsis.
They behave the same as on the wall: tap to select, double-tap to open
the inspector.

If a scene number appears in **more than one shoot day** in the
one-liner (a long scene split across two days), the card appears as a
full tile in each of those days — it is not deduplicated. This is the
intended behaviour; the same scene genuinely belongs to both days.

Small badges in the top-right corner of a card:

| Badge | Meaning |
|---|---|
| Orange **hand** | Card has been manually assigned to this day (§9.5) |
| Cyan **waveform** | Manual assignment AND sound report data exists for this day |
| Coloured **dot** | Revision colour from the script (§5.5) |

### 9.4.3 Placeholder cards

Scenes from the one-liner that have **no matching card** on the wall
appear as placeholder tiles — dashed border, greyed text, orange **?**
badge. They carry the scene number, set and one-liner description from
the PDF.

Placeholders are read-only. To turn a placeholder into a real card,
import the script and make sure the scene number matches, or manually
create a card and assign it to the day (§9.5).

### 9.4.4 Unmatched tiles section

Cards on the wall that appear in **no** shoot day — neither by schedule
match nor by manual assignment — collect in an **Unmatched Tiles** strip
at the bottom of the schedule. The orange header shows the count.

Assign an unmatched card to a day by right-clicking it (🍎 macOS) or
long-pressing it (📐 iPadOS) and choosing a shoot day from the menu, or
by dragging it onto a day section (§9.5.2).

## 9.5 Moving Cards Between Days

### 9.5.1 Context menu

Right-click a card (🍎 macOS) or long-press a card (📐 iPadOS) to open
the context menu:

| Option | What it does |
|---|---|
| **Move This Tile to Shoot Day…** | Reassigns this one card to the chosen day |
| **Move This and All Below to Shoot Day…** | Reassigns this card and every card below it in the current day's order |
| **Clear Manual Assignment** | Removes the override; card reverts to schedule matching |
| **Remove from Schedule** | Removes this scene entry from the day entirely (card stays on wall) |

**Move N Selected Tiles to Shoot Day…** replaces the single-tile option
when multiple cards are selected (§9.5.4).

### 9.5.2 Drag to a day

Drag any card and drop it onto a different day section. The day
highlights in blue while you hold the card over it. Release to
assign. You can drag a multi-selection this way — all selected cards
move together.

### 9.5.3 Clear a manual assignment

A manually assigned card stays on the chosen day even if a new
one-liner is imported that would put it elsewhere. To revert to
schedule-driven placement, right-click → **Clear Manual Assignment**.

### 9.5.4 Multi-select and bulk move

To move several cards at once:

**🍎 macOS:**
- **⌘-click** individual cards to toggle them.
- **Shift-click** to extend the selection to a range.

**📐 iPadOS:**
- Tap one card to select it, then tap others to add them.

A selection bar appears at the top of the schedule showing the count
and a **Move to Shoot Day…** menu. Choose a day to move all selected
cards in one step. The selection bar also has an **✕** button to
deselect all.

> ✱ **Tip** — use **Move This and All Below to Shoot Day…** from the
> context menu to quickly slide a block of scenes from one day to
> another without selecting them individually.

## 9.6 Report Badges

Each day header can show up to one badge per report type. Badges are
added when you attach a shoot report (§10); they give a quick visual
status of what has been imported for each day.

| Badge colour | Report type |
|---|---|
| Teal | Sound |
| Indigo | Camera |
| Orange | Continuity |
| Purple | Call Sheet |
| Green | Essentials |

**Tap or click a badge** to open the attached file. On 📐 iPadOS a
QuickLook preview opens; on 🍎 macOS the file opens in the system
default app.

**Right-click a badge** for a context menu with **Open** and
**Remove** options. Removing a badge deletes the report attachment
record from the document (the file inside the package is not deleted).

## 9.7 Searching in Schedule Mode

The search bar filters the day view in real time. Matching is across:

- Scene number (e.g. `14`, `14b`, `1/14`, `01-14`)
- Set description
- One-liner text
- Card description and synopsis

Type `1/14` or `01-14` to find scene 14 in episode 1 specifically.
Days that have no matching scenes are hidden while the search is active.
The **Unmatched** section is also filtered.

Clear the search to return to the full schedule view.

## 9.8 How Matching Works

Scene Cards matches each schedule entry to a card using normalised
scene numbers:

1. **TV format** — `ep-scene` e.g. `01-14`, `1-14a`. Matches a card
   whose `sceneDisplay` normalises to the same string.
2. **Film format** — bare scene number e.g. `14`, `14A`. Matches any
   card with that scene number across all episodes.

Normalisation strips leading zeros, converts separators (`/`, `.`) to
dashes, and removes part labels (`pt1`, `pt2`). The match is
case-insensitive.

A card that has been **manually assigned** to a day (§9.5) always
appears on that day regardless of what the one-liner says. In the day
where the schedule originally placed it, the slot shows as a placeholder
until the manual assignment is cleared.

A scene that appears in **two shoot days** in the one-liner (split
scene) renders as a full card in both days with no manual action needed.
The Unmatched section at the bottom correctly excludes it.

## 9.9 Persistence

The imported schedule and all manual day assignments are saved inside
the document:

- The `OneLinerSchedule` (shoot days, scene entries, date strings) is
  stored in `payload.json` alongside the wall state.
- Manual assignments (`manualScheduleDay`) are stored in the wall state
  and survive script re-imports (§5.1.2).
- Report attachment records are stored in the wall state; the report
  files themselves live in `Media/reports/Day_NN_DDMMYY/{type}/` (§10.7).

Opening the document on another machine restores the full schedule view
without re-importing the PDF.

## 9.10 Where to Go Next

- **Attach sound, camera and continuity reports** — see §10 *Shoot
  Reports*.
- **Print the wall** — Schedule mode is not currently printable; use
  Scenes mode for printing. See §11.
- **Multi-episode scene numbers** — see §13 *Multi-Episode*.
- **Switching between wall modes** — keyboard shortcuts in §16.
