<!--
TODO — still open for this chapter:
  1. Screenshots — the import panel showing matched/unmatched sections,
     the shoot reports day+type filter chips, the result banner.
  2. RESOLVED — basic card metadata (brief, description, comments,
     location, revision colour, omitted status) transfers automatically
     for every matched card. There is no checkbox to suppress it.
     performImport() always applies these fields unconditionally.
     §12.3 updated to document this as always-on behaviour.
  3. RESOLVED — Import Session Data is macOS-only. It does not appear
     in the iPadOS ⋯ overflow menu. The command is registered via
     SceneCardsCommands (macOS menu bar only); the notification listener
     in ContentView has no iOS entry point. §12.1 updated with 🍎 badge.
-->

# Chapter 12 — Import Session Data

**Import Session Data** copies content from one Scene Cards document
into the document you are working on. You choose the source document,
select which categories of data to bring across, and confirm — Scene
Cards matches scenes by number, transfers the selected content, and
leaves everything else untouched.

Typical uses:

- Pulling sound reports collected in a day-file into the main production
  document.
- Copying reference photos, thumbnails or script text from one episode
  document into another.
- Merging a revised schedule (one-liner and manual day assignments) from
  a coordinator's copy into your own.
- Absorbing new scenes from a colleague's document that don't yet exist
  on your wall.

> ⓘ **Note** — Import Session Data requires an active subscription or
> a free trial. It is not available after the trial has expired.

## 12.1 🍎 macOS — Opening the Import Panel

Import Session Data is a macOS feature. It is not available on iPadOS
in the current version.

1. Open the document you want to import **into** (the destination).
2. Choose `File → Import Session Data…` (`⌘⌃I`).
3. In the file picker, select the Scene Cards document to import
   **from** (the source). Click **Open**.

The import panel opens, headed with the source document name. It
analyses the source and groups content into sections based on what is
available to transfer.

## 12.2 How Cards Are Matched

Before you make any selections, Scene Cards compares the source and
destination walls and divides source cards into two groups:

**Matched cards** — source cards whose episode, scene number and suffix
(e.g. `A`, `B`) correspond to a card already on your wall. Data from
these cards can be merged into the matching destination card.

**Unmatched cards** — source cards with no counterpart on your wall.
These can be added as new cards (§12.3.7).

Matching is case-insensitive and treats episode 0 as a wildcard
(matches any episode in the other document). Scene numbers are
normalised the same way as schedule matching (§9.8).

## 12.3 Selecting What to Import

For all matched cards, basic metadata transfers **automatically** — no
toggle required. The following fields are always overwritten on each
matched card:

- Brief
- Description
- Comments
- Location
- Revision colour
- Omitted status

Beyond that, each additional category has its own toggle or set of
checkboxes. Nothing else imports until you click **Import**. You can
select any combination.

### 12.3.1 Reference files

Copies files from the source card's reference carousel (§8) into the
matching destination card. Existing references on the destination are
kept — the import is additive, not a replacement.

The section lists each matched card that has references. Expand a card
to toggle individual files; use **Select All** to take everything.

> ⓘ **Note** — the destination document must be saved before reference
> files can be copied. If it has not been saved yet, this section is
> unavailable.

### 12.3.2 Thumbnails (hero stills)

Copies the still image shown on the face of each card (§7). Overwrites
any existing still on the destination card.

Toggle individual cards or use **Select All**.

### 12.3.3 Script text

Copies the raw screenplay text for each matched scene. Overwrites the
destination card's existing script text entirely.

Toggle individual cards or use **Select All**.

### 12.3.4 Schedule

Two independent toggles:

**One-Liner Schedule** — replaces the destination's entire shoot
schedule with the source's. The toggle shows the number of shoot days
in the source.

**Manual Day Assignments** — copies per-card day overrides (the orange
hand badges in Schedule mode, §9.5) for all matched cards. Overwrites
any existing overrides on matched cards; cards with no source override
are left as they are.

> ⚠ **Caution** — importing the one-liner schedule replaces the
> destination schedule entirely. Any shoot days or scene entries that
> exist in the destination but not in the source will be lost.

### 12.3.5 Shoot reports

Transfers report attachment records and the per-card sound data for
matched cards.

Two filters control what transfers:

**Report types** — choose any combination of Sound, Camera, Continuity,
Call Sheet and Essentials.

**Shoot days** — choose which shoot days to bring across. Each day
shows the number of files and sound entries it contains. Days default
to none selected — you must pick at least one.

Only reports that satisfy **both** filters are transferred. For each
selected day and type:

- The report file is copied into `Media/reports/` in the destination
  package (skipped if a file with the same name already exists there).
- The attachment record is updated (any existing record for that day,
  type and filename is replaced).
- For sound reports, per-card entries for the selected shoot days are
  replaced with the source entries.

See §10.6 for more on how shoot reports travel between documents.

### 12.3.6 Document settings

**Character colours** — copies the character-name-to-colour mappings
(used for card highlighting). Source values overwrite destination values
where the character name matches; unmatched names are added.

**Excluded characters** — merges the source's excluded character list
into the destination's. No characters are removed from the destination.

### 12.3.7 New cards (unmatched scenes)

Source cards that have no match on the destination wall appear here.
Toggle individual cards or use **Add All as New Tiles** to select
the whole group.

Each selected card is added to the destination wall with a fresh ID.
All card data travels with it — scene number, description, still,
references, script text, sound entries and so on. New cards fill
available slots in the wall grid; existing cards are not reordered.

## 12.4 Conflict Handling at a Glance

| Category | When data already exists on the destination |
|---|---|
| Basic metadata | Always overwritten (automatic) |
| Reference files | Kept — import is additive |
| Thumbnail | Overwritten by source |
| Script text | Overwritten by source |
| One-liner schedule | Overwritten entirely |
| Manual day assignments | Overwritten for matched cards |
| Report files | Skipped if the same filename exists |
| Report attachment records | Replaced (matched by day, type, filename) |
| Per-card sound entries | Replaced for selected shoot days |
| Character colours | Overwritten by source (per character name) |
| Excluded characters | Merged — destination list grows, nothing removed |
| New cards | Always added with a fresh ID |

## 12.5 Undoing an Import

Import Session Data is undo-able. Press `⌘Z` immediately after
importing to revert all changes made in that session. Each import
category is wrapped in its own undo group, so a single `⌘Z` reverses
the entire import in one step.

> ⚠ **Caution** — file copies (reference files and report files
> written into the package) are **not** reversed by undo. The undo
> removes the references to those files from the document state, but
> the files themselves remain in the package. Use **Show Package
> Contents** in Finder to remove them manually if needed.

## 12.6 Where to Go Next

- **Shoot reports** — see §10 for how reports are structured and what
  is stored per shoot day.
- **Reference files** — see §8 for the carousel and file types.
- **Schedule and day assignments** — see §9.
- **Document package layout** — see §4.8.
