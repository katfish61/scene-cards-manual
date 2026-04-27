# Appendix C — Sample Workflows

Four end-to-end workflows showing how the features of Scene Cards
combine in practice. Each assumes you are starting from the described
point; cross-references point to the detailed procedure in the relevant
chapter.

---

## C.1 Feature Film: From Script to Printed Wall

**Starting point:** You have a locked PDF script and a folder of
location stills. You want a physical wall for the first production
meeting.

1. **Create a new document.** `⌘N` (🍎) or the New Document button
   (📐📱). Save immediately (`⌘S` on 🍎, or via the Files browser on
   📐📱) so the package exists on disk.

2. **Import the script.** `File → Import Script PDF or FDX…` (`⌘⇧I`).
   Select the PDF. Scene Cards creates one card per scene heading.
   Review the wall — any scene with a non-standard heading will be
   missing and can be added manually (§5.2). See §5.1.

3. **Check numbering.** If the script is a single-episode feature,
   all cards will be episode 0 (film/pilot convention). Confirm scene
   numbers are correct; use **Renumber From Here** if anything is off
   (§5.4.2).

4. **Add synopses.** The first action line is pre-filled as a starting
   synopsis. Replace it with a one-liner beat for each scene that needs
   one (§6.4). This is optional but useful for the wall to be readable
   at a glance.

5. **Batch import stills.** `File → Batch Import Images (Folder)…`
   (`⌘⌥I`). Select the folder. Scene Cards matches images to cards by
   filename — name your files `Scene_5.jpg`, `Scene_12A.jpg` etc. for
   automatic matching (§7.3).

6. **Arrange the wall.** Drag cards to reorder if needed, or use
   **Move Tile** in the inspector to position a card after a specific
   scene number (§6.5). Switch to **Locations mode** (`⌘⇧2`) to
   verify INT/EXT groupings read correctly, then switch back to
   **Scenes mode** (`⌘⇧1`).

7. **Print.** `⌘P` → choose your printer → Print. The wall prints
   A4 portrait, 2 columns × 3 rows per page. OMITTED cards print with
   a label so the page count stays honest (§11).

---

## C.2 TV Series: Multi-Episode Setup and Scheduling

**Starting point:** You have PDFs for two or more episodes of a series
and a one-liner strip board for the shoot block.

1. **Create a new document** and save it.

2. **Import the first episode script.** `⌘⇧I`. Before confirming,
   make a note of the episode number — you will need to set it on the
   imported cards. After import, select all cards for that episode
   (§3.6.1), open the inspector, and confirm the Episode field reads
   the correct number. If it imported as episode 0 (the default),
   select all and change them (§6.2, §6.8).

   Repeat for each episode, importing scripts one at a time and
   checking episode numbers as you go. See §13.2.

3. **Arrange episodes on the wall.** By default, all episodes land in
   one continuous sequence. Use the wall width control to give each
   episode its own row-set if you prefer them visually separated
   (§13.3).

4. **Import the one-liner.** `File → Import Script PDF or FDX…` is
   for scripts; for the one-liner use the **Schedule** workflow:
   switch to Schedule mode (`⌘⇧3`) and use **Import One-Liner** (📐)
   or `File → Import One-Liner PDF…` (🍎). Select the strip board PDF.
   Scene Cards matches cards by scene number. See §9.1–9.2.

5. **Check Unmatched.** The bottom of Schedule mode lists any schedule
   entries that did not match a card (§9.4.4). Common causes: episode
   number mismatch (TV format `1-14` vs film format `14`) or
   non-standard scene numbers. Assign unmatched cards manually by
   dragging them onto a day header (§9.5).

6. **Set character colours.** Open the Script Panel (🔍) for any key
   scene and tap character names to assign colours. Colours propagate
   across every scene that character appears in (§6.9).

---

## C.3 On-Set: Daily Sound Report Integration

**Starting point:** You are using Scene Cards during a shoot block.
At the end of each day the sound department provides a folder of
reports.

1. **At the start of the block**, ensure the wall is set up with cards
   numbered to match the shoot script, and a one-liner has been
   imported so Schedule mode shows shoot days (§9.1).

2. **End of shoot day — import sound reports.** `File → Import Sound
   Reports from Folder…`. Select the folder of PDFs or CSVs from the
   sound department. Scene Cards reads the filename of each file to
   extract episode and scene number, then attaches takes to the
   matching card. See §10.2.

3. **Check coverage.** In Schedule mode, each day header shows a 🔵
   or 🟠 badge when sound data is present (§9.6). Click through to
   cards with data and expand **Shoot Data** in the inspector to verify
   takes are attaching to the right scenes (§6.7).

4. **Handle mismatches.** If takes are landing on the wrong card, the
   most likely cause is a scene number mismatch between the report
   filename and the card. Check the filename format your recorder uses
   (§10.5) and correct the card's scene number if needed (§6.2).

5. **Attach call sheets and essentials.** Use the day header **↓doc**
   button in Schedule mode to attach the day's call sheet and
   essentials PDF to the correct shoot day (§10.4). These are stored
   in the package but not parsed.

6. **Sync to iPad.** If iCloud Drive is enabled (§14.1), save the
   document (`⌘S`) and the updated file will sync within a few minutes.
   Any on-set iPad or iPhone will show the latest sound data without any
   manual transfer.

---

## C.4 Script Revision: Merging a New Draft

**Starting point:** You have a working Scene Cards document with stills,
synopses, and reference files attached. The writer delivers a revised
draft — new scenes, omitted scenes, location changes.

1. **Import the revised script.** `⌘⇧I`. Select the new PDF. Scene
   Cards runs the re-import merge (§5.1.2):
   - Cards that match by episode + scene number are **updated** —
     their location and script text are overwritten with the new
     draft's values, but synopses, stills, and reference files are
     preserved.
   - New scene headings become **new cards** added to the end of the
     wall.
   - Cards with no corresponding heading in the new draft are **not
     automatically deleted** — they stay on the wall unchanged.

2. **Review revision colours.** Cards from the new draft carry the
   revision colour extracted from the PDF (§5.7). Switch to Scenes
   mode and scan for goldenrod, blue, or pink cards — these are the
   scenes that changed.

3. **Handle omissions.** Scenes that disappeared from the new draft
   remain as cards. If a scene is confirmed omitted, select its card
   and press **Toggle OMITTED** (`⌘⌥O`). This keeps the number slot
   on the wall while flagging the scene visually (§5.5). If the scene
   is simply renumbered, update the scene number in the inspector
   (§6.2).

4. **Place new cards.** Newly created cards land at the end of the
   wall. Use **Move Tile** in the inspector (§6.5) to position each
   one after its correct predecessor.

5. **Update synopses for changed scenes.** Synopses survive re-import
   unchanged, which means a scene that was substantially rewritten will
   still carry its old synopsis. Review the revised script text in the
   Script Panel (§3.5) and update synopses where needed (§6.4).

6. **Print an updated wall** for distribution (`⌘P`). The revision
   colour shows on the printed cards, so recipients can see at a glance
   which scenes changed (§11).
