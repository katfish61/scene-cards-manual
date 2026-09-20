<!--
TODO — still open for this chapter:
  1. Screenshot still needed: the result banner after a completed import.
     Save under Docs/Manual/assets/.
-->

# Chapter 12 — Import Project Data

**Import Project Data** pulls content from one Scene Cards document into the document you have open. You pick the source, choose which categories to bring across, and confirm. Scene Cards matches cards by scene number, transfers what you selected, and leaves everything else untouched.

Common uses:

- Pulling sound, camera, or continuity reports from a day-file into the main production document.
- Copying stills or reference photos from one episode into another.
- Merging a revised schedule from a coordinator's copy into your own.
- Adding scenes from a colleague's document that don't yet exist on your wall.

> ⓘ Import Project Data requires an active subscription or a free trial.

---

## 12.1 Opening the import panel

You always import **into** the document that is currently open. The document you pick in the next step is the **source** — the one you're pulling from.

**macOS**

Choose `File → Import Project Data…` (`⌘⌃I`). In the file picker, select the source document and click **Open**.

**iPhone / iPad**

Tap **⋯** in the toolbar → **Import Project Data…**. In the document picker, tap the source file to select it.

The import panel opens with the source document name at the top. Scene Cards analyses both documents and groups the available content into sections.

---

## 12.2 How cards are matched

Before you choose anything, Scene Cards compares the two documents and splits the source cards into two groups:

**Matched cards** — source cards whose episode, scene number, and suffix (A, B, etc.) correspond to a card already on your wall. These are the cards you can selectively merge data from.

**Unmatched cards** — source cards with no counterpart on your wall. You can add these as new cards (§12.3.7).

Matching is case-insensitive. Episode 0 acts as a wildcard — it matches any episode in the other document.

---

## 12.3 Choosing what to import

### Basic metadata — always transferred

For every matched card, the following fields are **always** copied from the source, with no toggle:

- Brief (scene heading)
- Description
- Comments / one-liner
- Location
- Revision colour
- Omitted status

You cannot suppress this. If you open the import panel and hit Import, these fields update on every matched card.

### 12.3.1 Reference files

Copies files from the source card's reference carousel (§8) into the matching destination card. Existing references on the destination are kept — this import is **additive**, not a replacement.

The section lists each matched card that has references. Expand a card to choose individual files, or tap **Select All** to take everything.

> ⓘ The destination document must be saved before reference files can be copied. If it is unsaved, this section is unavailable.

### 12.3.2 Thumbnails (hero stills)

Copies the still image shown on the face of each card (§7). The source image overwrites any existing still on the destination card.

Toggle individual cards or use **Select All**.

### 12.3.3 Script text

Copies the raw screenplay text for each matched scene. The source text overwrites the destination card's existing script text entirely.

Toggle individual cards or use **Select All**.

### 12.3.4 Schedule

Two independent toggles:

**One-Liner Schedule** — replaces the destination's entire shoot schedule with the source's. The toggle shows how many shoot days the source contains.

**Manual Day Assignments** — copies per-card day overrides (the hand badges in Schedule mode, §9.5) for all matched cards. Overwrites any existing overrides on matched cards; cards with no source override are left as they are.

> ⚠ Importing the one-liner schedule replaces the destination schedule entirely. Any shoot days or scene entries that exist in the destination but not the source will be lost.

### 12.3.5 Shoot reports

Transfers report attachments and per-card sound data for matched cards.

Two filters control exactly what transfers:

**Report types** — pick any combination of Sound, Camera, Continuity, Call Sheet, and Essentials.

**Shoot days** — pick which shoot days to bring across. Each day shows the number of files and sound entries it contains. Days default to none selected — you must choose at least one.

Only reports that satisfy **both** filters are transferred. For each selected day and type:

- The report file is copied into the destination package (skipped if a file with the same name already exists there).
- The attachment record is updated — any existing record for that day, type, and filename is replaced.
- For sound reports, per-card entries for the selected shoot days are replaced with the source entries.

See §10.6 for more on how shoot reports travel between documents.

### 12.3.6 Document settings

**Character colours** — copies character-name-to-colour mappings. Source values overwrite destination values where the character name matches; unmatched names are added.

**Excluded characters** — merges the source's excluded character list into the destination's. No characters are removed from the destination.

### 12.3.7 New cards (unmatched scenes)

Source cards that have no match on the destination wall appear here. Toggle individual cards, or tap **Add All as New Cards** to select the whole group.

Each added card arrives with a fresh ID and all its data — scene number, description, still, references, script text, sound entries, and so on. New cards fill available empty slots in the wall grid; existing cards are not reordered.

---

## 12.4 Conflict handling at a glance

| Category | What happens if data already exists on the destination |
|---|---|
| Basic metadata | Always overwritten |
| Reference files | Kept — import is additive |
| Thumbnail | Overwritten by source |
| Script text | Overwritten by source |
| One-liner schedule | Replaced entirely |
| Manual day assignments | Overwritten for matched cards |
| Report files | Skipped if same filename already exists |
| Report attachment records | Replaced (matched by day, type, filename) |
| Per-card sound entries | Replaced for selected shoot days |
| Character colours | Overwritten per character name |
| Excluded characters | Merged — destination list grows, nothing removed |
| New cards | Always added with a fresh ID |

---

## 12.5 Undoing an import

Import Project Data is undoable. Press `⌘Z` immediately after importing to revert all the changes made in that session. The entire import is wrapped in a single undo group — one `⌘Z` reverses it all.

> ⚠ File copies (reference files and report files written into the package) are **not** reversed by undo. The undo removes the references to those files from the document, but the files themselves remain in the package. Use **Show Package Contents** in Finder to remove them manually if needed.

---

## 12.6 Where to go next

- **Shoot reports** — how reports are structured and what is stored per shoot day: §10.
- **Reference files** — the carousel and supported file types: §8.
- **Schedule and day assignments** — §9.
- **Document package layout** — §4.8.
- **Collaborating** — the merge workflow when two people have worked on separate copies: §14.3.
