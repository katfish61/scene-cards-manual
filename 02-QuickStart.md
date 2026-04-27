<!--
TODO — still open for this chapter:
  1. Sample script — not currently shipped. Consider adding a short
     "PaperEdit-Demo.pdf" under Docs/Manual/assets/ so readers have something
     to try immediately.
-->

# Chapter 2 — Quick Start

This chapter gets a brand-new production into Scene Cards in about ten
minutes. By the end you will have a document on disk, a wall populated from a
script PDF, a still on one of the cards, and everything saved.

If you already have Scene Cards open on a document, skip to §2.3.

**Before you start**

- Scene Cards installed and launched (Chapter 1).
- A script in **PDF** or **Final Draft (`.fdx`)** format, or the sample
  script shipped with the app.
- A still image (JPEG, PNG or HEIC) for at least one scene — a phone photo
  is fine.

## 2.1 Create a New Document

A Scene Cards document holds one production. On a series, one document can
cover every episode — see §13 *Multi-Episode Productions*.

### 2.1.1 🍎 macOS

1. Launch Scene Cards. The standard **Open a Document** dialog appears.
2. Choose `File → New` (`⌘N`). The document opens immediately with an
   empty wall.
3. Save the document with `File → Save…` (`⌘S`). Choose a location — iCloud
   Drive is a sensible default for a production that will travel between
   devices — and give it a name such as `MyProduction.scenecards`.

> ✱ **Tip** — macOS auto-saves the document after the first manual save. You
> rarely need to press `⌘S` again; use `File → Save As…` (`⇧⌘S`) only when
> you want to fork a copy.

### 2.1.2 📐 iPadOS

1. Launch Scene Cards. The Files browser appears (after the Welcome screen
   on first run — see §1.6.2).
2. Tap the **+** button at the top centre of the Files browser. A new
   document is created with an empty wall.
3. To rename, tap and hold the document's title in the toolbar and type a
   new name, or rename later from the Files app.

> ⓘ **Note** — iPadOS auto-saves continuously. There is no manual Save
> command; closing the document commits the latest state.

### 2.1.3 📱 iPhone

1. Launch Scene Cards. The Files browser appears.
2. Tap **Create Document** in the Files browser. A new document is created
   with an empty wall — 3 cards wide in portrait by default.
3. Rename from the Files app at any time.

> ⓘ **Note** — iPhone auto-saves continuously, the same as iPadOS.

## 2.2 Import a Script PDF

A script import walks the document top-to-bottom, finds every scene heading
(e.g. `INT. OFFICE – DAY`), and creates one card per scene. The script text,
scene number, episode number, location and any detectable character names
are read across in a single pass.

Scene Cards accepts:

- **PDF** — the most common format from screenwriting software.
- **Final Draft (`.fdx`)** — native, parsed directly from the XML.

### 2.2.1 🍎 macOS

1. Choose `File → Import Script PDF or FDX…`.
2. Select one or more files in the Open panel. Multi-select is supported —
   you can import several episodes of a series in one go.
3. Click **Open**. A progress indicator appears while the script is parsed.
4. When parsing completes, the wall populates with one card per scene, in
   script order.

### 2.2.2 📐📱 iPadOS and iPhone

1. Tap the **⋯** overflow menu in the top-right of the toolbar.
2. Choose **Import Script PDF or FDX…**.
3. Pick the script file from the Files picker.
4. Tap **Open**. The wall fills as parsing completes.

> 🔒 **Permission required** — the first time you pick a file outside the
> app's own folder, the system asks whether Scene Cards may read it. Tap
> **Allow**.

### What gets imported

For each scene the parser extracts:

| Field              | Source in the script                                    |
|--------------------|---------------------------------------------------------|
| Scene number       | The number printed in the scene heading                 |
| Episode number     | Detected from cover page or filename where possible     |
| Location / Slugline | The scene heading itself (`INT. / EXT.` plus location) |
| Raw script text    | Every line between this heading and the next           |

Characters detected in dialogue are added to the document's colour palette
— see §6.3 *Character Detection & Colour Assignment*.

> ⚠ **Caution** — a script whose scene headings use non-standard formatting
> (e.g. lower-case or unnumbered) may produce cards the parser couldn't
> number automatically. See §5 *Building the Wall* for how to renumber or
> re-brief them.

## 2.3 Open a Scene Card

Every card on the wall opens into an **Inspector** where you can edit its
content.

### 2.3.1 Opening the inspector

A single click (or tap) on a card **selects** it — the usual behaviour for
wall operations like reordering or revision-colour changes. The Inspector
itself is opened in one of two ways:

- **🍎 macOS** — **double-click** the card, or click it once to select and
  then click the **Inspector** button at the top-right of the toolbar.
- **📐 iPadOS / 📱 iPhone** — **double-tap** the card. The Inspector slides
  up as a sheet.

### 2.3.2 Fields on the Inspector

From top to bottom:

- **Scene Number** — three fields: **Episode / Scene / Suffix**. Editable
  if the parser got any of them wrong.
- **Location** — the slugline (`INT. OFFICE`). Auto-uppercased.
- **Synopsis** — free-form notes on the scene. Populated from the script's
  first action line on import; edit to taste.
- **References** — carousel of attached reference files (§8).
- **Move Tile** — shortcut to reposition the card after another scene by
  number.
- **Toolbar strip** — Import Image, Omit/Unomit, Insert After, Renumber
  From Here, Close Gap, Delete.

Sound-report entries, when present, appear below the toolbar as a
**Shoot Data** block. Day-level reports live in Schedule mode — see §10.

> ⓘ **Note** — the card's **revision colour** and script-derived heading
> come from the import and are not edited in the inspector. To change them,
> re-import from an updated PDF or FDX (§5.1).


### 2.3.3 Closing the inspector

- **🍎 macOS** — click the **Inspector** button at the top-right of the
  toolbar to toggle the panel closed.
- **📐 iPadOS / 📱 iPhone** — tap the **Inspector** button at the
  top-right of the toolbar, or swipe the sheet down.

> ✱ **Tip** — edits are committed as soon as a field loses focus. You do
> not need to "save" an individual card.

## 2.4 Add a Still

Stills live on the card itself and double as the thumbnail on the wall.

### 2.4.1 Drag a file onto the card

- **🍎 macOS** — drag a still from Finder, Photos or a folder window onto
  any card. The image is copied into the document and becomes the card's
  thumbnail. Supported formats: **JPEG, PNG, HEIC/HEIF, TIFF, GIF, WebP,
  BMP** and most common **RAW** formats (CR2, NEF, ARW).
- **📐 iPadOS / 📱 iPhone** — use the Inspector route in §2.4.2.
  Drag-and-drop from Photos onto a card is technically supported but
  fiddly on touch devices; the Inspector is faster and more reliable
  for a single still.

### 2.4.2 Use the Inspector

1. Open the card's Inspector (§2.3).
2. Click or tap the **Import Image** button (photo icon) in the
   inspector's toolbar strip.
3. Choose a file from the picker.

### 2.4.3 Batch-assign a folder of stills

If you already have a folder of on-set or scout photos named by scene
number, Scene Cards can match and assign them in one go.

- **🍎 macOS** — `File → Batch Import Images (Folder)…` and pick the folder.
- **📐 iPadOS / 📱 iPhone** — **⋯** overflow → **Import Images from
  Files…**, then navigate to the folder.

Filenames that start with a scene number are matched onto the wall —
`5.jpg`, `5A.jpg`, `005_rehearsal.jpg` all land on scene 5 (or 5A). The
parser reads the leading digits and an optional letter suffix; anything
after that (underscore, dash, space, dot, bracket) is treated as
descriptive padding and ignored. To pin a photo to a specific episode
in a multi-episode document, prefix the filename with `Ep{NN}_Scene_`
— e.g. `Ep01_Scene_5.jpg` lands on episode 1, scene 5. See §7.3
*Batch Import from a Folder* for the full matching rules.

> ⓘ **Note** — stills are stored inside the `.scenecards` package under
> `Media/thumbnails/`. They travel with the document and never need a
> separate sync.

## 2.5 Save and Close

### 2.5.1 🍎 macOS

- **Save** — `⌘S`. Redundant after the first save, but available.
- **Close** — `⌘W`, or click the window's red close button. The document
  saves automatically on close.
- **Reopen** — it appears in `File → Open Recent` and in the macOS Stage
  Manager / Recents view.

### 2.5.2 📐📱 iPadOS and iPhone

- **Close** — tap the back chevron (or back button on iPhone) in the
  top-left of the toolbar. The document commits and returns you to the
  Files browser.
- **Reopen** — tap the document in the Files browser.

## 2.6 Next Steps

You now have a working Scene Cards document with scenes and at least one
still. From here:

- **Organise the wall** — see §5 *Building the Wall* for reordering,
  omissions and revision colours.
- **Add reference material** — see §8 *Reference Files* for scouts,
  storyboards and research.
- **Build a schedule** — see §9 *Scheduling* for importing a one-liner and
  working in Schedule mode.
- **Browse the interface** — see §3 *Orientation* for a guided tour of the
  toolbar, inspector and script panel.
