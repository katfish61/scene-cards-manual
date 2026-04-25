# Appendix B — Glossary

Terms used in this manual, in alphabetical order.

---

**Batch import**
An import operation that processes a folder of files in one step rather
than picking files individually. Scene Cards supports batch import for
images (§7.3) and sound reports (§10.2.3).

**Card**
The user-facing term for a single scene in Scene Cards. A card occupies
one slot on the wall and holds the scene number, location, synopsis,
stills, reference files, and shoot data for that scene. Internally
referred to as a *tile* in the codebase — that term is never used in
this manual.

**Carousel**
The horizontal scrolling row of thumbnails at the top of the inspector
that shows the reference files attached to a card. Navigate with the
chevron buttons (🍎) or by swiping (📐).

**Close Gap**
An action that removes a card from its slot and shifts every subsequent
card one position to the left, closing the empty space. The inverse of
inserting a blank card. Undoable with `⌘Z`. See §5.3.3.

**Episode**
An integer stored on each card that groups scenes by TV episode. Episode
0 is the conventional value for films and pilots. Scene numbers display
as `EP/SCENE` (e.g. `02/14A`). See §13.

**FDX**
Final Draft XML — the native file format of Final Draft screenwriting
software. Scene Cards reads `.fdx` files directly as an alternative to
PDF import. See §5.1 and Appendix A.

**FileWrapper**
A macOS / iOS framework type that presents a directory on disk as a
single document. Scene Cards uses a FileWrapper package for its
`.scenecards` format — the OS shows it as one file, but it is a folder
containing `payload.json` and the `Media/` directory. See §18.1.

**Hero still**
The primary image displayed on a card face — a production still,
location photograph, storyboard frame, or any image you assign to
represent a scene. Stored in `Media/thumbnails/`. See §7.

**Import Session Data**
A macOS-only feature that merges selected data (stills, references,
shoot reports, etc.) from one Scene Cards document into another. Used
to consolidate work done on separate devices or by separate crew
members. See §12.

**Inspector**
The panel that shows and edits the fields of a single selected card.
Opens as a right-hand sidebar on 🍎 macOS or a bottom sheet on 📐
iPadOS. See §6.

**Location mode**
One of three wall views. Cards are grouped into columns by their
location string; empty groups are hidden. Accessed with `⌘⇧2` or the
📍 button. See §3.2.

**Multi-select**
A selection of two or more cards. When multiple cards are selected, the
inspector switches to the Multi-Select Panel, which allows bulk moves
but not per-field edits. See §6.8.

**OCR (Optical Character Recognition)**
Text extraction from image-based PDFs using Apple's Vision framework.
Scene Cards falls back to OCR when PDFKit cannot extract selectable text
from a script or one-liner PDF. An orange badge marks schedule entries
that relied on OCR. See §9.4.4.

**OMITTED**
A card state that marks a scene as cut from the production. An OMITTED
card remains on the wall (preserving the slot and number) but is visually
distinguished and excluded from character and report tallies. See §5.5.

**One-liner**
A condensed strip-board document — typically one line per scene — used
by production to schedule shoot days. Scene Cards parses a one-liner PDF
to populate Schedule mode. Also called a *strip board*. See §9.1.

**payload.json**
The primary data file inside a `.scenecards` package. A JSON-encoded
`Payload` struct that holds all wall state, tile data, schedule
information, and shoot report metadata. See §18.3.

**Reference file**
Any file attached to a card for production reference — storyboards,
location photos, rehearsal video, script PDFs, shot lists, etc. Stored
in `Media/references/` inside the document package. See §8.

**Renumber From Here**
An action that walks the wall starting at the selected card and
re-issues sequential scene numbers, preserving suffixes. Used to
resync numbering after cards have been inserted or moved. See §5.4.2.

**Revision colour**
A colour applied to a card to indicate which script revision it belongs
to — matching the coloured paper used in physical script revisions
(white, goldenrod, blue, pink, green, etc.). Set automatically during
script import; cannot be changed in the inspector. See §5.7.

**Scene heading**
The formatted scene identifier line in a screenplay:
`INT. OFFICE — DAY`. Scene Cards extracts the location portion
(`INT. OFFICE`) and stores it in the card's location field (§6.3).
Also called a *slugline*.

**Scene mode**
The default wall view. Cards appear in a continuous left-to-right,
top-to-bottom grid. Accessed with `⌘⇧1` or the 🎬 button.

**Schedule mode**
One of three wall views. Cards are grouped by assigned shoot day, with
day headers showing the shoot date, crew call, and page count. Accessed
with `⌘⇧3` or the 📅 button. See §9.

**Script Panel**
A sidebar that displays the raw script text extracted from the PDF for
the currently selected scene. Also the interface for assigning character
colours. Toggled with the 🔍 button on 📐 iPadOS, or the left sidebar
control on 🍎 macOS. See §3.5 and §6.9.

**Security-scoped bookmark**
A macOS mechanism that allows Scene Cards to re-open a file or folder
outside its sandbox on subsequent launches, without requiring the user
to pick it again. Used for reference folders linked from external
locations. See §8.3.

**Shoot day**
A numbered day in the production schedule, populated from the one-liner
import. Cards are assigned to shoot days either automatically (by scene
number matching) or manually. See §9.

**Shoot data**
Sound report entries that have been parsed and attached to a card —
displayed in the Shoot Data block at the bottom of the inspector. See §6.7.

**Slot**
A fixed position on the wall grid. A slot is either empty or occupied
by one card. Slots are numbered sequentially left-to-right, top-to-bottom.
The mapping of slots to cards is stored in `slotToTile` in `payload.json`.

**Slugline**
See *Scene heading*.

**Sound Devices**
A brand of professional audio recorder widely used in film and TV
production. Scene Cards parses sound reports exported from Sound Devices
recorders as PDF or CSV. See §10.2 and Appendix A.

**Strip board**
See *One-liner*.

**Subscription**
Scene Cards is sold as an annual subscription through the App Store.
A 7-day free trial gives full access to all features. After the trial
ends without a subscription, documents open in read-only mode. See §1.7.

**Suffix**
An optional letter or letters appended to a scene number to indicate an
inserted scene (`7A`, `7B`, `7AA`). Stored separately from the scene
number integer; auto-uppercased on entry. See §6.2.

**Synopsis**
A free-form text field on each card for a production note or scene
description. Not overwritten by script re-import (unlike the location
and heading fields). Labelled *Comments* in the underlying file format.
See §6.4.

**Tile**
The internal / developer term for what this manual calls a *card*. Used
throughout the Swift codebase (`Tile.swift`, `tilesByID`, etc.) but not
in any user-facing text.

**Trial**
See *Subscription*.

**UTType**
Apple's Uniform Type Identifier system for declaring file formats. The
Scene Cards document type is `com.keithtunney.scenecards`. See §18.2.

**Vision**
Apple's on-device machine learning framework, used by Scene Cards for
OCR when a PDF cannot be read as selectable text. See *OCR*.

**Wall**
The main working area — a grid of cards representing the scenes of a
production. The default width is 8 columns on 🍎 macOS and 6 on 📐
iPadOS; width is adjustable by pinching on iPadOS. See §3.1.

**Zaxcom Nomad**
A brand of professional audio recorder. Scene Cards parses sound reports
from Zaxcom Nomad recorders as PDF. See §10.2 and Appendix A.
