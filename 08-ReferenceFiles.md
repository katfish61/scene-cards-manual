<!--
TODO — still open for this chapter:
  1. Screenshots — the inspector References section showing the carousel
     (empty state, a PDF tile, a video tile, a folder tile), the
     macOS "Add Files and Folders…" open panel, the iOS Add… menu.
  2. RESOLVED — "Link a Folder" on iPadOS does NOT maintain a live link.
     The referenceFolderBookmark resolution path is #if os(macOS) only.
     On iPadOS, the FolderPicker calls importRefURLs() → copyReferenceImages(),
     which copies files into the package. iCloud/duplication is a non-issue
     because the files travel inside the package like any other import.
     §8.2.5 has been updated to reflect this.
  3. RESOLVED — the "Save Document First" alert fires for New Note and
     New Drawing only (both openNoteEditor/openDrawingEditor guard on
     documentURL ?? store.projectRootURL != nil). Drop and Add Files
     have no such guard — they stage files in memory when the doc is
     unsaved. §8.2.1 caution note and §8.3 caution are accurate as written.
-->

# Chapter 8 — Reference Files

A **reference file** is any file attached to a card that is not the
card's hero still. One card can hold any number of references: a PDF
storyboard, a location scout folder, a continuity photo, a sound note,
a video clip — whatever the scene needs. They sit in a scrollable
carousel in the inspector and travel inside the document package.

This chapter covers getting files onto a card (drag, import button,
camera, drawing, note), the types that are supported, how to view and
remove them, and where they live on disk. The hero still — the single
image shown on the face of the card — is in §7.

---

## 8.1 What Counts as a Reference File

Anything that is not the still. Common examples:

- Storyboard PDFs
- Location-scout photos (extra angles, coverage shots)
- Continuity photos
- Video tests or tone pieces
- Audio files (scratch dialogue, ambient recordings)
- Text notes
- Sketch drawings
- Word, Excel or Pages documents
- Folders of on-set dailies or watch-folder exports

A card's still (§7) is drawn from `stillImageData` and shown on the
wall thumbnail. References live separately in `Media/references/` and
are only visible inside the inspector. Both can exist on the same card
at the same time.

## 8.2 Attaching Reference Files

### 8.2.1 Drop files onto the carousel

Open the inspector for a card (§6.1), then drag any file or folder from
Finder (🍎 macOS) or Files (📐 iPadOS split-view) onto the **References**
area. A green border appears while the drop is in flight.

- Dropped files are copied into the document package immediately.
- You can drop multiple files in one go — each lands as a separate carousel
  tile, ordered by filename.
- Dropping a **folder** copies the whole folder as a single unit; it
  appears in the carousel as a folder tile (§8.5.3).

> ⚠ **Caution** — if the document has not been saved yet, dropped files
> are held in memory for the current session but are not written into a
> package folder. Save the document first (`⌘S`) to make the attachment
> permanent.

### 8.2.2 🍎 macOS — Add Files and Folders…

1. Open the inspector and scroll to the **References** section.
2. Click **Add Files and Folders…** (the `+` button).
3. In the Open panel, select any files or folders and click **Open**.

The panel accepts multiple selections. Files are copied into the package;
folders are copied as a single unit.

### 8.2.3 📐 iPadOS — Add… menu

Tap the **Add…** button in the References toolbar to reveal three options:

| Option | What it does |
|---|---|
| **Choose from Photos** | Opens the Photos picker. Select up to 20 images or videos. |
| **Choose from Files** | Opens the Files app. Navigate to any file and tap to attach it. |
| **Link a Folder** | Picks a folder; copies all its files into the package (§8.2.5). |

> 🔒 **Permission required** — "Choose from Photos" requires Photos access
> (Settings → Privacy → Photos). "Choose from Files" prompts the first time
> you reach a location outside the app's sandbox.

### 8.2.4 📐 iPadOS — Camera

Tap the **camera** button in the References toolbar to shoot directly from
the device camera. The photo is saved into the document package as a JPEG
and added to the carousel immediately.

> ⓘ **Note** — the camera button only appears on devices that have a camera
> available. iPads with a rear camera show it; simulator builds do not.

### 8.2.5 Link a Folder (iPadOS)

**Link a Folder** opens a folder picker. Every file inside the chosen
folder is copied into the document package, exactly as if you had
selected them individually with **Choose from Files**. The files travel
inside the package from that point on — there is no live link back to the
original folder.

Use this as a shortcut when you want to pull in an entire folder of
scout photos or video clips in one tap rather than selecting items
individually.

## 8.3 Creating Notes and Drawings

In addition to importing existing files, Scene Cards can create new
reference items directly inside the inspector.

### 8.3.1 New Note

A note is a plain-text (`.txt`) file stored in the card's reference
folder. It appears in the carousel as an inline scrollable text tile.

**🍎 macOS** — click **New Note…** in the References toolbar. A floating
editor panel opens. Type your note, then click **Save** to write it into
the package, or **Cancel** to discard. The note appears in the carousel
straight away.

**📐 iPadOS** — notes are created from the **Add…** menu. *(Confirm
availability in current build.)*

> ⚠ **Caution** — notes and drawings require the document to be saved
> first. If you tap **New Note…** or **New Drawing…** on an unsaved
> document, Scene Cards shows a "Save Document First" alert. Save
> (`⌘S`), then try again.

### 8.3.2 New Drawing

A drawing is a PencilKit sketch saved as a PNG into the card's reference
folder.

**🍎 macOS** — click **New Drawing…** in the References toolbar. A
floating drawing panel opens. Sketch with the mouse or a connected
graphics tablet. Click **Save** when done.

**📐 iPadOS** — tap the **pencil tip** button in the References toolbar.
If an image is currently showing in the carousel, it loads as a
background layer so you can annotate directly over it (useful for
marking up a still or a location photo). Tap **Save** to commit.

## 8.4 Viewing and Navigating References

All reference files for a card appear in the **carousel** — the large
tile inside the References section of the inspector.

### 8.4.1 Navigate between files

- **🍎 macOS** — click the left/right chevrons at the edges of the
  carousel, or scroll horizontally with a trackpad gesture over the
  carousel area.
- **📐 iPadOS** — swipe left or right across the carousel.

The **N / N** counter in the header (e.g. `2 / 5`) shows the current
position and total count. Dot indicators below the carousel show up to
12 positions; an ellipsis (`…`) appears when there are more.

### 8.4.2 What each tile type shows

| File type | Carousel appearance |
|---|---|
| Image (`jpg`, `png`, `heic`, etc.) | Full-bleed preview; tap to open in the system viewer |
| PDF | First-page preview with a red **PDF** badge; tap to open |
| Video (`mp4`, `mov`, etc.) | Poster frame with a **VIDEO** badge; tap the play button to play inline |
| Audio (`mp3`, `m4a`, `wav`, etc.) | Waveform icon with filename and format badge; **Play / Stop** button |
| Note (`.txt`, `.md`) | Inline scrollable text; **NOTE** badge |
| Document (`docx`, `xlsx`, `key`, etc.) | File icon and filename; tap to open in the system app |
| Folder | Folder icon and name; single-click to reveal in Finder (🍎) or browse in Files (📐) |
| Unknown | Generic file icon and filename |

### 8.4.3 Open a file in its native app

- **🍎 macOS** — click **Open in App** in the References toolbar, or
  single-click a PDF or document tile. The file opens in whichever
  app the OS associates with that type (Preview, Acrobat, Final Cut,
  etc.) while Scene Cards stays in the foreground.
- **📐 iPadOS** — tap any file tile. Scene Cards posts a QuickLook
  preview for supported types; for files the OS can't preview inline,
  it hands off to the Files app or the registered handler.

For **folder** tiles:
- **🍎 macOS** — single-click to open in Finder (background). Double-click
  to open and bring Finder forward.
- **📐 iPadOS** — tap to browse the folder in Files.

### 8.4.4 Share or export (iPadOS)

Tap the **share** button (⬆) in the References toolbar to open the
standard iOS share sheet for the currently visible file. Use this to
AirDrop a scout photo, save a PDF to Files, or send a note by email.

## 8.5 Removing a Reference File

1. Navigate the carousel to the file you want to remove.
2. Tap the **trash** button (🗑) in the References toolbar.

The file is deleted from the document package immediately. There is no
confirmation dialog.

`⌘Z` does **not** restore a deleted reference in the current build —
the deletion is a direct filesystem remove, outside the undo stack.
Keep a copy elsewhere if the file is important.

> ⚠ **Caution** — removing a reference cannot be undone. If you need
> to keep the file, export it first (🍎: **Open in App** and save from
> there; 📐: share sheet → Save to Files) before deleting.

## 8.6 Supported File Types

Scene Cards accepts any file the OS can identify. Internally the check
is `MediaManager.isMediaFile`, which maps file extensions to a media
category. Files that don't match any known extension land in the
**unknown** category and still attach — they show a generic icon and
open in whatever app the OS uses.

Recognised types by category:

| Category | Extensions |
|---|---|
| Image | `jpg`, `jpeg`, `png`, `heic`, `heif`, `tiff`, `tif`, `gif`, `webp`, `bmp`, `raw`, `cr2`, `nef`, `arw` |
| PDF | `pdf` |
| Video | `mp4`, `mov`, `m4v`, `avi`, `mkv`, `webm` |
| Audio | `mp3`, `m4a`, `aac`, `wav`, `aiff`, `flac`, `ogg`, `opus` |
| Note | `txt`, `md`, `markdown` |
| Document | `doc`, `docx`, `xls`, `xlsx`, `ppt`, `pptx`, `odt`, `ods`, `odp`, `pages`, `numbers`, `key`, `rtf`, `csv`, `tsv` |
| Folder | Any directory |

Files and folders that don't match any extension above are still accepted
and attach as **unknown** tiles — they can be opened and deleted, they
just don't get a rich preview.

> ⓘ **Note** — the batch-image import paths (`File → Batch Import Images`,
> `⋯ → Import Images from Files…`) only match image extensions. Reference
> file import via the inspector accepts everything in the table above.

## 8.7 Where Reference Files Live on Disk

Reference files are copied into the document package at:

```
MyProduction.scenecards/
└── Media/
    └── references/
        ├── Ep01_Scene_5/
        │   ├── 001_scout_wide.jpg
        │   ├── 002_storyboard.pdf
        │   └── 003_location_notes.txt
        ├── Ep01_Scene_12B/
        │   └── 001_rehearsal_clip.mp4
        └── Ep02_Scene_3/
            └── 001_Set_Photos/        ← a copied folder
                ├── IMG_0001.jpg
                └── IMG_0002.jpg
```

**Folder naming** follows the episode-aware convention used throughout
the package (§4.8): `Ep{NN}_Scene_{N}{suffix}`. Each card gets its own
subfolder. Episode 0 writes as `Ep00_`.

> ⓘ **Note** — older documents written before the episode-aware build
> may have `Scene_5/` rather than `Ep01_Scene_5/`. Scene Cards reads
> both; new writes always use the episode-aware form.

**File naming** — each file is prefixed with a zero-padded sequence
number (`001_`, `002_`, …) followed by the original filename. This
preserves the import order and avoids collisions when two files share
the same name.

```
001_scout_wide.jpg
002_storyboard.pdf
003_notes.txt
```

A dropped or imported folder is copied as a single directory with the
same sequence prefix:

```
004_Set_Photos/
```

Files created by **New Note** are named `Note_YYYY-MM-DD_HH-mm-ss.txt`.
Files created by **New Drawing** are named `Drawing_YYYY-MM-DD_HH-mm-ss.png`.

## 8.8 Reference Files and Scene Re-import

When you re-import a script (§5.1.2), reference files on cards that
match by episode + scene number survive unchanged. The re-import only
replaces metadata derived from the script (synopsis, location, revision
colour, script text) — it does not touch the `Media/references/` folder.

A card that is *deleted* by the re-import (because its scene no longer
exists in the new draft) loses its reference folder along with
everything else. Mark a scene **OMITTED** (§5.5) before re-importing
if there is any chance it returns and you want to keep its references.

## 8.9 Where to Go Next

- **Import shoot reports** (sound, camera, continuity, call sheets) —
  see §10 *Shoot Reports*.
- **Print the wall** — references do not appear on the printed wall;
  only the still does. See §11 *Printing and Export*.
- **Document package layout** — see §4.8.
- **Hero stills** (the card's thumbnail image) — see §7.
