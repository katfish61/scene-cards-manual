<!--
TODO — still open for this chapter:
  1. Screenshots — the iPadOS navigation bar (annotated), the ⋯ overflow
     menu open, the inspector reference toolbar, the inspector tile
     action buttons.
  2. Confirm which individual tile-editing actions (synopsis, location,
     revision colour) are Pro-gated vs available in read-only mode.
     Read-only blocks all editing at the document level; need to check
     whether any editing survives in the trial-expired state.
  3. Confirm the exact SF Symbol / visual appearance of each mode button
     on iPadOS (film / location / calendar) for screenshot annotations.
-->

# Chapter 15 — Toolbar and Menu Reference

This chapter is a quick-reference listing of every control in Scene
Cards — the menu bar on macOS, the navigation bar on iPadOS, and the
inspector toolbar on both platforms. For step-by-step procedures see
the relevant chapter; this chapter is a lookup table.

Items marked ★ require an active subscription or free trial (§1.7).

---

## 15.1 🍎 macOS — Menu Bar

Scene Cards has no floating toolbar on macOS. All commands are in the
menu bar.

### File

| Item | Shortcut | What it does |
|---|---|---|
| New | `⌘N` | Creates a new Scene Cards document |
| Open… | `⌘O` | Opens an existing document |
| Save | `⌘S` | Saves the document |
| Save As… | `⌘⇧S` | Saves a copy under a new name or location |
| Import Script PDF or FDX… ★ | `⌘⇧I` | Imports scenes from a Fountain / FDX / PDF script |
| Batch Import Images (Folder)… ★ | `⌘⌥I` | Imports a folder of images, matched by scene number |
| Batch Import Images (Select Files)… ★ | `⌘⌥⇧I` | Opens a file picker to import individual images |
| Import Sound Reports from Folder… ★ | — | Batch-imports sound report PDFs across shoot days |
| Import Session Data… ★ | `⌘⌃I` | Merges data from another Scene Cards document (§12) |
| Print Wall Layout… | `⌘P` | Prints the scene wall as an A4 grid (§11) |

### Edit

| Item | Shortcut | What it does |
|---|---|---|
| Undo | `⌘Z` | Undoes the last action |
| Redo | `⌘⇧Z` | Redoes the last undone action |
| Cut | `⌘X` | Cuts selected text |
| Copy | `⌘C` | Copies selected text |
| Paste | `⌘V` | Pastes from clipboard |
| Select All | `⌘A` | Selects all tiles or all text |
| Insert Tile After | `⌘⌥N` | Inserts a blank card after the selected card |
| Toggle OMITTED | `⌘⌥O` | Marks or unmarks the selected card as OMITTED |
| Renumber From Here | `⌘⌥R` | Renumbers all cards from the selection forward |

### View

| Item | Shortcut | What it does |
|---|---|---|
| Scenes | `⌘⇧1` | Switches to Scenes mode |
| Locations | `⌘⇧2` | Switches to Locations mode |
| Schedule | `⌘⇧3` | Switches to Schedule mode |

### Help

| Item | Shortcut | What it does |
|---|---|---|
| Scene Cards Quick Start… | `⌘⇧?` | Opens the Quick Start guide |
| Keyboard Shortcuts… | `⌘/` | Opens the keyboard shortcuts reference |
| User Manual… | — | Opens this manual in a browser |

---

## 15.2 📐 iPadOS — Navigation Bar

The navigation bar runs across the top of the screen. Controls are
split between the leading (left) and trailing (right) sides.

### Leading controls

| Control | What it does |
|---|---|
| **Script panel** — page with magnifier | Toggles the left script-text sidebar. Icon fills when open. |
| **⋯** — circle with three dots | Opens the overflow menu (§15.2.1) |

### Trailing controls

| Control | What it does |
|---|---|
| **Scenes** — film-reel icon | Switches to Scenes mode. Icon fills when active. |
| **Locations** — map-pin icon | Switches to Locations mode. Icon fills when active. |
| **Schedule** — calendar icon | Switches to Schedule mode. Icon fills when active. |
| **Inspector** — right-sidebar icon | Toggles the inspector sheet. Icon fills when open. |

### Search

Tap the search bar (displayed below the navigation bar) to filter
cards in real time by scene number, location, description or synopsis.
See §9.7 for Schedule mode search behaviour.

### 15.2.1 ⋯ Overflow menu

| Item | What it does |
|---|---|
| Undo | Undoes the last action |
| Import Script PDF or FDX… ★ | Imports scenes from a script file |
| Import Images from Files… ★ | Opens the Files picker to import images |
| Import from Photos… ★ | Opens the Photos picker to import images |
| Import Shoot Reports… ★ | Opens a folder picker for shoot report import (§10) |
| Print… | Prints the scene wall (§11) |
| Try Scene Cards Pro Free for 7 Days… | Opens the subscription paywall (shown when trial inactive) |
| Manage Subscription… | Opens subscription management (shown when subscribed) |

---

## 15.3 Inspector

The inspector opens as a right-hand sidebar (🍎 macOS) or a bottom
sheet (📐 iPadOS). It has two sections of controls: the **References
toolbar** at the top and the **Tile actions** at the bottom.

### 15.3.1 References toolbar

Controls for attaching and viewing reference files (§8).

| Control | Platform | What it does |
|---|---|---|
| Add Files and Folders… | 🍎 | Opens a file picker; copies files into the card's reference folder |
| New Note… | 🍎 | Opens a floating text editor; saves a `.txt` note into the reference folder |
| New Drawing… | 🍎 | Opens a drawing canvas; saves a PNG into the reference folder |
| Add… | 📐 | Menu: Choose from Photos / Choose from Files / Link a Folder |
| Camera | 📐 | Takes a photo and adds it directly to the carousel |
| Pencil (draw) | 📐 | Opens PencilKit canvas; loads the current carousel image as a background layer |
| ← → chevrons | 🍎 | Navigate between files in the carousel |
| Open in App | 🍎 | Opens the current file in its default system app |
| Share ⬆ | 📐 | Opens the share sheet for the current carousel file |
| Trash 🗑 | Both | Removes the current file from the carousel (no undo — §8.5) |

### 15.3.2 Tile action buttons

Controls that act on the card itself, below the carousel.

| Button | What it does |
|---|---|
| Import Image to Tile | Opens an image picker to set this card's hero still (§7) |
| Mark / Unmark OMITTED | Toggles the OMITTED state on the card |
| Insert Tile After | Adds a blank card immediately after this one |
| Renumber From Here | Renumbers all cards from this one forward |
| Close Gap | Removes this card from its slot without leaving a blank space |
| Delete Tile | Permanently deletes the card and all its attached media |

> ⚠ **Caution** — Delete Tile cannot be undone past the current
> session. Close Gap can be undone with `⌘Z`.

---

## 15.4 Where to Go Next

- **Keyboard shortcuts** — full table in §16.
- **Settings and Preferences** — see §17.
- **Subscription and trial** — see §1.7.
