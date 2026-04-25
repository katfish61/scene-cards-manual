<!--
TODO — still open for this chapter:
  1. Add a minimal worked example of a real payload.json with one tile,
     one shoot day and one sound entry, once a sample document is
     available for the manual assets folder.
  2. Document TileImageRef struct fields (preferredFilename, uuid etc.)
     once confirmed — not fully read in this pass.
-->

# Chapter 18 — File Format Specification

A `.scenecards` document is a **macOS/iOS FileWrapper package** — a
directory that the OS presents as a single file. You can inspect its
contents by right-clicking in Finder and choosing **Show Package
Contents**.

This chapter is a technical reference for the format. You don't need
to read it to use Scene Cards — it is here for anyone who wants to
inspect, back up, or write tooling against the file.

## 18.1 Package Layout

```
MyProduction.scenecards/
├── payload.json          ← all document state (JSON)
├── Images/               ← legacy image store (older documents)
└── Media/
    ├── thumbnails/       ← hero stills, one file per card
    ├── references/       ← reference files, one folder per card
    └── reports/          ← shoot report files, organised by day and type
```

`Images/` exists in documents created before the episode-aware build.
New writes use `Media/thumbnails/` exclusively. Scene Cards reads both.

`Media/` is preserved verbatim across saves — the app never rewrites
it, only adds to it. Removing a file from `Media/` via Finder is safe
and is the correct way to reclaim disk space (§10.7, §8.7).

## 18.2 UTType

| Key | Value |
|---|---|
| Identifier | `com.keithtunney.scenecards` |
| File extension | `.scenecards` |
| iCloud container | `iCloud.com.keithtunney.scenecards` |
| Conforms to | `com.apple.package` |

## 18.3 payload.json — Top Level

The file is a JSON-encoded `Payload` struct.

| Key | Type | Notes |
|---|---|---|
| `wallState` | object | See §18.4 |
| `savedAt` | ISO 8601 string | Timestamp of the last save |
| `appVersion` | string | App build version at save time |
| `oneLinerSchedule` | object \| null | Present when a one-liner has been imported; see §18.6 |

## 18.4 WallState

The core document state inside `wallState`.

| Key | Type | Notes |
|---|---|---|
| `rows` | integer | Grid height (always 6 in current builds) |
| `cols` | integer | Grid width (default 8 macOS, 6 iPadOS) |
| `tilesByID` | object | Map of UUID string → Tile object |
| `slotToTile` | object | Map of slot integer (string key) → UUID string |
| `revision` | integer | Incremented on every edit; used for dirty detection |
| `characterColours` | object | Map of character name → hex colour string e.g. `"#FF6B35"` |
| `excludedCharacters` | array of strings | Character names hidden from report views |
| `manualScheduleDay` | object | Map of tile UUID string → shoot day integer |
| `reportAttachments` | array | See §18.7 |

`slotToTile` is the wall layout — slot 0 is top-left, slots increase
left-to-right then top-to-bottom. A slot with no entry is empty.

## 18.5 Tile

Each entry in `tilesByID` is a Tile object.

| Key | Type | Notes |
|---|---|---|
| `id` | UUID string | Primary key |
| `episode` | integer | Episode number; 0 = film / pilot |
| `sceneNumber` | integer | Scene number |
| `sceneSuffix` | string \| null | Up to 3 characters, e.g. `"A"`, `"AA"` |
| `isOmitted` | boolean | True = card is marked OMITTED |
| `brief` | string | One-line description |
| `descriptionText` | string | Full scene description |
| `comments` | string | Production notes |
| `location` | string | e.g. `"INT. OFFICE"` |
| `scriptText` | string | Raw scene text extracted from the script PDF |
| `revisionColor` | string \| null | Revision colour name e.g. `"goldenrod"`, `"blue"` |
| `updatedAt` | ISO 8601 string | Last edit timestamp |
| `image` | object \| null | Reference to thumbnail file in `Media/thumbnails/` |
| `stillImageData` | base64 string \| null | Legacy inline image data (older documents) |
| `referenceFolderBookmark` | base64 string \| null | macOS security-scoped bookmark for reference folder |
| `soundEntries` | array | See §18.7 |
| `cameraEntries` | array | See §18.7 |
| `continuityEntries` | array | See §18.7 |

All fields except `id`, `episode`, `sceneNumber`, `rows` and `cols`
use `decodeIfPresent` with sensible defaults, so older documents open
cleanly in newer builds.

## 18.6 OneLinerSchedule

Present in `payload.oneLinerSchedule` when a schedule has been imported.

| Key | Type | Notes |
|---|---|---|
| `shootDays` | array of ShootDay | |
| `importedAt` | ISO 8601 string | When the one-liner was imported |
| `sourceFilename` | string | Original PDF filename |
| `usedOCR` | boolean | True if Vision OCR was used during import |

**ShootDay:**

| Key | Type | Notes |
|---|---|---|
| `id` | UUID string | |
| `number` | integer | e.g. `9` |
| `date` | string | e.g. `"Thursday, September 16, 2021"` |
| `crewCall` | string | e.g. `"06h30 - 17h30"` |
| `totalPages` | string | e.g. `"6 7/8"` |
| `scenes` | array of ScheduledScene | |

**ScheduledScene:**

| Key | Type | Notes |
|---|---|---|
| `id` | UUID string | |
| `sceneNumber` | string | e.g. `"2-19"`, `"1-14a"` |
| `set` | string | e.g. `"INT. HOSPITAL WARD"` |
| `oneLiner` | string | Scene description from the strip board |
| `intExt` | string | `"INT"`, `"EXT"`, `"I/E"` |
| `dayNight` | string | `"Day"`, `"Night"`, `"Eve"`, `"Dawn"` |
| `pages` | string | e.g. `"1 2/8"` |
| `storyDay` | string | e.g. `"SD4"` |
| `castNumbers` | array of integers | Cast numbers from the strip board |
| `isStandby` | boolean | True if listed under a STANDBY header |
| `location` | string | Left-column location label |

## 18.7 Shoot Report Data

**ShootReportAttachment** (entries in `wallState.reportAttachments`):

| Key | Type | Notes |
|---|---|---|
| `id` | UUID string | |
| `shootDay` | integer | Shoot day number |
| `type` | string | `"Sound"`, `"Camera"`, `"Continuity"`, `"Call Sheet"`, `"Essentials"` |
| `filename` | string | Original filename of the report file |
| `importedAt` | ISO 8601 string | |
| `entryCount` | integer | Number of parsed entries (0 for attach-only types) |
| `fileBookmark` | base64 string \| null | Security-scoped bookmark to reopen the file |

**SoundEntry** (entries in `tile.soundEntries`):

| Key | Type |
|---|---|
| `id` | UUID string |
| `shootDay` | integer |
| `filename` | string |
| `reel` | integer |
| `take` | integer |
| `duration` | string |
| `tracks` | string |
| `notes` | string |
| `circled` | boolean |
| `sourceFile` | string \| null |

**CameraEntry** and **ContinuityEntry** follow the same pattern with
their respective fields as described in §10.3.

## 18.8 Media Folder Layout

```
Media/
├── thumbnails/
│   ├── Ep01_Scene_27.jpg     ← current episode-aware form
│   └── Scene_5.png           ← legacy form (older documents)
├── references/
│   ├── Ep01_Scene_27/
│   │   ├── 001_storyboard.pdf
│   │   └── 002_location.jpg
│   └── Ep02_Scene_14A/
│       └── 001_rehearsal.mp4
└── reports/
    ├── Day_01_160921/         ← dated form (Day_NN_DDMMYY)
    │   ├── sound/
    │   ├── camera/
    │   ├── continuity/
    │   ├── callsheets/
    │   └── essentials/
    └── Day_02/                ← legacy form (no date)
        └── sound/
```

Reference files are prefixed with a zero-padded sequence number
(`001_`, `002_`, …) to preserve import order and avoid name collisions.

## 18.9 Format Compatibility

Scene Cards reads three historical formats in order:

1. **Current package** — directory with `payload.json` (standard)
2. **Flat autosave** — a single JSON file containing the full `Payload`
3. **Legacy WallState** — raw `WallState` JSON without the `Payload`
   wrapper (migrated automatically on open)

All `Tile` fields use `decodeIfPresent`, so a document saved by an
older build opens in a newer build without error — missing fields
receive their defaults. There is no explicit version number in the
format; forward compatibility is maintained by additive-only changes.
