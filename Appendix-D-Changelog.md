# Appendix D — Changelog

Release notes for Scene Cards, most recent first. The version number
shown here matches the number in **Scene Cards → About Scene Cards**
(🍎) or **Settings → Scene Cards** (📐).

---

<!--
  HOW TO ADD AN ENTRY
  ===================
  Copy the template below, fill in the version, date, and bullet points,
  and paste it at the top of the list (above the previous release).

  Categories to use (omit any that are empty):
    ### New
    ### Improved
    ### Fixed
    ### Removed

  Keep bullets short — one line per change. Cross-reference the manual
  section if the change affects documented behaviour (e.g. "See §9.1").
-->

---

## 1.8.2 — August 2026

### New
- **Call sheets now parse and schedule** — previously attach-only, Call
  Sheet import reads the planned scene list and reschedules matching
  cards, the same way Sound and Continuity already did. The shoot day
  is read straight off the call sheet's own page, so single-file
  imports no longer need it entered manually. See §10.2.3.

### Improved
- **Continuity is now the authoritative schedule source.** Where a
  call sheet's plan and a continuity log's record of what was actually
  shot disagree, Continuity always wins. Importing either a Call Sheet
  or a Continuity report now **replaces** that day's scene list rather
  than adding to it — any card that isn't confirmed by the new import
  moves to the Unmatched section (§9.4.4) instead of staying behind,
  so schedule mode reflects what production actually did rather than
  accumulating every plan that changed along the way. See §10.2.3.
- Folder import (`File → Import Reports from Folder…`) auto-classifies
  Call Sheet and Continuity files individually, alongside Sound and
  Camera, instead of routing everything non-Sound/Camera through a
  single generic pipeline. Call sheet files are grouped and scheduled
  under each file's own detected shoot day, so a folder bundling more
  than one day's call sheets no longer lumps them together. See §10.1.2.

### Fixed
- A card evicted from a day by a Call Sheet or Continuity re-import
  could keep reappearing as a placeholder rather than moving cleanly
  to Unmatched, because clearing its manual day assignment alone did
  nothing when the card was also still matched by the schedule's own
  scene list for that day. Eviction now overrides both.

---

## 1.7.0 — July 2026

### New
- **Edit heading and action in the script panel** — Edit mode shows pinned
  **Scene Heading** and **Action** rows above the script body. Changes appear
  immediately in the inspector, on tiles, and in print. Manually edited
  headings survive script re-import (the merge summary reports how many were
  kept); Location is never touched, so Locations-mode grouping is unaffected.
  See §6.4.1.
- **Full scene headings everywhere** — cards in all wall modes and the
  printed wall now show the whole scene heading, never truncated. Print shows
  the full script heading (previously the short location label); when a card
  has a still, the image shrinks to make room rather than cutting the text.
  See §11.1.2.
- **Unified report folder import** (🍎) — `File → Import Reports from Folder…`
  takes a whole day folder of mixed paperwork and auto-detects each file's
  type: sound reports schedule the day's scenes, camera sheets and continuity
  paperwork file into the reference carousels. The shoot day is pre-filled
  from the folder name (sd3, SD48, Day_03). See §10.1.2.
- **Import Sound Report Files** (🍎) — `File → Import Sound Report Files…`
  imports individual sound report PDFs/CSVs with per-file day detection.
  See §10.1.3.
- **ZoeLog camera reports** — parsed into per-take entries (lens, stop,
  filters, shutter, FPS, notes) and filed per-scene into the reference
  carousels. See §10.2.2.
- **Zaxcom slate-based sound reports** — takes named by slate number
  (`1049T1`) are now resolved to scenes via production numbers in the Notes
  column. See §10.2.1.
- **Skip omitted scenes** — new print option, on by default, filters OMITTED
  cards out of the printout. The print sheet also gains an episode filter for
  multi-episode documents. See §11.1.3.
- **Remove Image** — new inspector button removes a card's hero still.
  See §6.6.

### Improved
- Cards show up to **four lines of action text** (was two), and the
  inspector's **Synopsis** field is renamed **Action**. See §6.4.
- Continuity logs that record "Shot on Day" now reschedule cards to the day
  the paperwork claims, even when it differs from the day entered at import.
  See §10.2.3.
- Shoot-day prompts accept SD-prefixed entries (`SD01`, `sd034`).
- Scene Number Format picker: select a format row, then click **Import**
  (previously tapping a row imported immediately). See §9.2.1.
- Move Tile panel: compact one-line layout with tappable matching-scene
  chips as you type. See §6.5.
- Continuity parser reads more real-world formats: colon-less `SCENE`
  labels, multi-scene lists, `Scene(s)` blocks, and underscore filenames.
- Phone-width walls widen to 8 columns when the document is opened on a Mac.
- Re-imported continuity reference files no longer duplicate in the carousel.

### Fixed
- **📐📱 Script panel dismissal** — the script panel now has a ✕ close button
  in its handle bar and can be swiped down to dismiss. Its height is clamped
  to the wall area, so it can no longer grow over the toolbar and hide the
  🔍 toggle — previously this could make the panel impossible to close,
  especially in Split View or Stage Manager. See §3.5.
- App no longer hangs when importing a single image to a card while the
  document has unsaved changes (🍎).
- Subscription falsely locking to read-only after an App Store update.
- Script import: part-numbered scenes (`3pt 1/2`) and numbered character
  names now import correctly.
- Slash-format schedules: recovered missing scene-8 rows and misread tokens;
  R/F world markers are matched and omitted scenes flagged.
- Teleprompter no longer goes dead after toggling Edit mode in the script
  panel.
- Print rendering: uneven borders, black edge lines, and image gaps in both
  layouts.
- Selection border now consistent across all three wall modes.

---

## 2026.9 — June 2026

### New
- **Print layout picker** — when printing the wall, a dialog now lets you choose
  between **6 per page** (A4, 2 × 3 grid) and **1 per page** (A6, one card per
  sheet). The 1-per-page option is ideal for printing individual scene cards on
  A6 index-card stock. Works on macOS and iOS. See §11.1.3.

---

## 2026.8 — May 2026

### Fixed
- **Stray scenes from stage directions** — text inside parentheses such as
  `(LOOK AS 0.29)` or `(2/8 pgs)` no longer produces phantom scenes. Both the
  Vision bounding-box pass and the text-based parser now walk paren depth per
  line and skip matches sitting inside an unclosed `(`.
- **Lost suffix letters on Cyrillic look-alikes** — when Vision OCR reads a
  suffix as its Cyrillic homoglyph (e.g. `0.03В` with Cyrillic `В` instead of
  Latin `B`), the suffix is now transliterated to Latin before matching, so the
  scene comes through as `0-3b` rather than collapsing to a bare `0-3`.
- **Multi-day "part" scenes** — scenes split across consecutive shoot days
  (e.g. `0.03pt 1/2` on one day and `0.03pt 2/2` on the next) are now retained
  on both days. Previously the cross-day clean-up step assumed one scene = one
  day and removed the second appearance.

---

## 2026.7 — May 2026

### Fixed
- **Missing dates on imported schedules** — one-liners whose End-of-Day banner
  uses a colon between the day number and the date (e.g. `End of Day # 43 :
  Monday, May 11, 2026 -- Total : 1 7/8 pgs`) now parse the date correctly.
  Previously the parser only recognised dash separators, so dates and page
  totals came through empty for these schedules.

---

## 2026.6 — May 2026

### Fixed
- **Scenechronize schedule import** — schedules exported from Scenechronize now
  import correctly. Two issues were resolved: (1) within-block episode numbering
  (e.g. ep 5, 6) is now automatically remapped to match full-season tile keys
  (e.g. ep 305, 306), so scenes are no longer stripped as unrecognised; (2) page
  count fractions written as `1/8pg` (no space) were being misread as scene
  numbers — they are now correctly ignored.

---

## 2026.5 — May 2026

### Improved
- **iOS dialogue layout** — dialogue lines in the script panel now sit in a
  properly centred column (≈ 56 % of panel width), with equal margins on both
  sides of the character cue, matching standard PDF/FDX screenplay layout.
  Previously dialogue was left-flush on iPhone and iPad.

### Fixed
- **Teleprompter snap-back** — pressing ▶ after manually scrolling to a new
  position no longer snaps the script back to where it was paused. Scrolling
  now resumes from the exact pixel the user scrolled to, on both macOS and iOS.
- **Dead play button after end of script** — once auto-scroll reached the last
  line, pressing ▶ had no effect. It now jumps back to the top and starts a
  fresh countdown.
- **macOS teleprompter jerkiness** — scrolling is now pixel-by-pixel (identical
  to iOS) rather than jumping one full line per second. The result is the same
  smooth, continuous motion on both platforms.

---

## 2026.4 — May 2026

### New
- **Script panel auto-scroll (teleprompter)** — a ▶ / ⏸ play button and
  two sliders (Delay 0–20 s, Speed 0.3 ×–5.0 ×) let you read any scene
  hands-free. Tap anywhere on the script text to toggle play/pause, just
  like a video player. Drag the script during playback to pause and
  reposition; press ▶ again to resume from the new position. Works on
  macOS and iOS. See §3.5.1.

### Improved
- **Delay control** replaced the previous +/− stepper with a slider
  (0–20 s, 1-second steps), giving fine resolution across the useful
  0–10 s range without fiddly small buttons.
- **Play button on iOS** is now full-size with a larger icon, making it
  easy to tap while holding a device on-set.

---

## 2026.3 — May 2026

### New
- **Reference thumbnail strip** — the dot indicators below the reference
  carousel have been replaced with a scrollable row of tappable thumbnails.
  Each cell shows a live preview (image, PDF cover, video poster frame) or a
  colour-coded file-type icon. Tap or click any thumbnail to jump directly to
  that file; the strip scrolls automatically to keep the active item centred.
  Works on both macOS and iOS. See §8.4.1.
- **Draw on Image — macOS** — the macOS drawing editor now supports loading
  the current carousel image as a background layer, matching the existing iOS
  behaviour. Open a card with an image in the carousel and click **New
  Drawing…**; the editor title changes to **Draw on Image** and the photo
  appears aspect-fit behind the canvas. The saved PNG composites the photo and
  your annotations together. Non-image carousel items (PDF, video, note, etc.)
  still open a blank canvas. See §8.3.2.

### Fixed
- Images and drawings in the reference carousel now resize correctly when the
  inspector panel is resized. Previously wide images could overflow the panel
  and push controls off-screen; this is resolved on both macOS and iOS.

---

## 2026.3 — May 2026

### New
- **macOS camera capture** — click the **camera** button in the
  References toolbar on Mac to open a camera sheet that supports both
  photo and video. Still frames are saved as JPEG; video clips as MOV.
  Both land directly in the carousel without leaving Scene Cards. See §8.2.3.
- **Schedule Merge** — importing a second one-liner PDF when a schedule
  is already loaded now prompts **Merge / Replace / Cancel** instead of
  silently replacing. Merge updates days with matching numbers, adds new
  days, and leaves unchanged days (and their attached reports) intact.
  See §9.2.2.
- **Cast numbers in day header** — when the one-liner includes cast
  columns, a green badge in each day header lists the sorted cast numbers
  for that shoot day. See §9.4.1.
- **Script title in script panel** — the script title detected from the
  PDF title page (e.g. revision colour + episode marker) is shown in
  italics in the script panel navigation bar. See §6.9.

### Improved
- **iOS camera supports video** — the camera button on iPhone and iPad
  now offers photo and video modes via the standard UIKit picker. Video
  clips are attached to the carousel exactly like any other import.
  See §8.2.5.
- **One-liner parser: numberless "End Day" format** — schedules that
  write "End Day — Wednesday, …" without a day number are now handled
  correctly. Day numbers are inferred from the nearest preceding
  "SHOOT DAY #N" header.
- **One-liner parser: date / total-pages extraction** — the date field
  no longer over-captures into the "Total Pages" suffix when both appear
  on the same line.

---

## 2026.2 — April 2026

### New
- **Import Project Data on iPhone and iPad** — the Import Project Data
  feature is now available on iOS via the **⋯** overflow menu. See §12.1.
- **Share Document… on iPhone and iPad** — **⋯ → Share Document…** opens
  the system share sheet for the current `.scenecards` file. AirDrop,
  Messages and Files receive the package intact; Mail wraps it in a zip
  (standard iOS/macOS behaviour). See §4.6.2.

### Improved
- **Stills now sync reliably via iCloud** — every import path (drag,
  batch folder, inspector photo button, Photos picker) now writes both
  an inline JPEG (max 800 px, quality 0.7) and an on-disk copy in
  `Media/thumbnails/`. The inline copy syncs instantly with the
  document; the on-disk copy is available for package-level tooling.
  Previously drag-and-drop stored only the inline copy and batch import
  stored only the on-disk copy. See §7.7.

### Fixed
- Reference folder viewer on iPhone and iPad could become stuck with no
  **Done** button visible after opening a folder from the inspector.
  Fixed — the Done button now dismisses reliably on all devices. See §8.4.3.

---

## 2026.1 — April 2026

### New
- **iPhone support** — Scene Cards now runs on iPhone (iOS 16.6 or
  later). All import, scheduling, and reference features are available.
  Wall defaults to 3 columns in portrait, 5 in landscape.
- **iCloud sync** — documents stored in iCloud Drive now sync
  automatically across Mac, iPad, and iPhone. See §14.1.
- **FDX import** — Final Draft `.fdx` files are now accepted by the
  script importer in addition to PDF. See §5.1 and Appendix A.

### Improved
- One-liner import now falls back to Vision OCR for image-rendered
  PDFs, with an orange badge indicating OCR was used. See §9.4.4.
- Schedule mode Unmatched section lists scene entries that could not
  be matched to a card. See §9.4.4.

### Fixed
- Reference folders were not preserved when a script was re-imported
  and a card's scene number had changed. Fixed — reference files now
  survive re-import as long as the episode + scene combination matches.

---

<!--  Older releases go below this line, newest first.  -->
