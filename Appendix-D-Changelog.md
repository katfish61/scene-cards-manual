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
- **Import Session Data on iPhone and iPad** — the Import Session Data
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
