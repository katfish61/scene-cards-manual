<!--
TODO — still open for this chapter:
  1. Screenshots — a wall showing cards from two episodes mixed together,
     the Inspector episode/scene/suffix fields, a card face showing the
     EP/SCENE format.
  2. RESOLVED — BlockSession (Blocksession.swift) and its supporting
     views (EpisodeSidebar, BlockScriptWallView, BlockLocationWallView)
     are fully implemented but never wired into the app UI. No mode
     button, no menu item, never instantiated. Development code only —
     nothing to document in the current version.
  3. RESOLVED — wall width is NOT a named setting. On iPadOS, users
     adjust columns via pinch-to-zoom (1–10 columns, stored in
     store.state.cols). On macOS the width is fixed at 8 columns with
     no user control. §13.4 corrected accordingly.
-->

# Chapter 13 — Multi-Episode Projects

Scene Cards assigns an episode number to every card. On a single-episode
or feature film project that number stays out of the way — but on a TV
series you can import several episodes into one wall and work across all
of them together. This chapter covers how episode numbers are assigned,
how the wall looks with multiple episodes, how to edit episode and scene
numbers in the inspector, and how episodes affect scheduling and
on-disk file naming.

## 13.1 Episode Numbers and Scene Display

Every card carries an integer episode number. The default for a new
blank card is episode **1**. A value of **0** means the project is a
film, pilot or special — use episode 0 when your script does not have
episode numbering.

The card face always shows episode and scene together in the format
`EP/SCENE`:

| Episode | Scene | Suffix | Displayed as |
|---|---|---|---|
| 1 | 27 | — | `01/27` |
| 2 | 14 | A | `02/14A` |
| 0 | 72 | — | `00/72` |
| 3 | 5 | — | `03/05 OMITTED` |

The episode is zero-padded to two digits. The suffix (A, B, AA, etc.)
is appended directly after the scene number, with no space.

## 13.2 Importing Multiple Episodes

### 13.2.1 Episode detection on import

When you import a script PDF (§5.1), Scene Cards reads the episode
number from the **filename first** — patterns like `Episode_2.pdf`,
`Ep02_Script.pdf` or `E02.pdf` are all recognised. If no episode
number is found in the filename, it falls back to the document text
(searching the first page for "Episode N" or "Ep N").

All scenes from a single import receive the same episode number. If
the PDF itself contains TV-format scene headings like `1.27` or
`2-05A` (episode.scene), the parser extracts both episode and scene
from the heading and assigns them independently per card.

### 13.2.2 First import

The first import onto an empty wall replaces any existing cards. Cards
are sorted by episode then scene number, so a multi-episode import
lands in running order.

### 13.2.3 Re-importing and adding a second episode

When you import a script onto a wall that already has cards, Scene Cards
merges rather than replacing:

- Cards from **the same episode** as the imported script are updated,
  added or removed to match the new draft.
- Cards from **other episodes** are left exactly where they are.

This means you can build up a multi-episode wall incrementally —
import Episode 1, then import Episode 2, and end up with cards from
both on the same wall. Episode 1 cards stay in their slots; Episode 2
cards are appended after them.

> ⓘ **Note** — a merge summary appears after each import, showing how
> many cards were added, updated, removed and unchanged for the affected
> episode.

> ⚠ **Caution** — re-importing an episode replaces all metadata for
> that episode's cards (synopsis, location, revision colour). Reference
> files, thumbnails and sound report data are preserved. See §5.1.2.

## 13.3 Editing Episode, Scene and Suffix

To change the episode number, scene number or suffix on a card:

1. Open the card's inspector (§6.1).
2. In the **Scene** row, edit the three fields: **Ep**, **Scene** and
   **Suffix**.
3. Press Return or click elsewhere to commit.

The card face updates immediately. Suffixes are trimmed to three
characters maximum.

> ⚠ **Caution** — changing a card's episode or scene number breaks the
> link between that card and its `Media/` folder (thumbnails, references,
> report entries). The files remain on disk but will not be found at the
> new scene key until the document is next saved and reopened. If you
> need to renumber a card, do it before attaching media.

## 13.4 The Wall With Multiple Episodes

All episodes live together on the same wall — there are no separate
tabs, sections or headers per episode. After importing two episodes the
wall shows Episode 1 cards followed by Episode 2 cards in a continuous
grid.

**Wall width and episode breaks** — on 📐 iPadOS you can adjust the
number of columns by pinching on the wall (1–10 columns). If you know
your episode length, pinch until the column count matches it — a
60-scene episode at 10 columns fills exactly 6 rows, creating a natural
visual break between episodes without any manual rearrangement. On
🍎 macOS the wall width is fixed at 8 columns.

There is no episode filter in the current version — all episodes are
always visible on the wall. Use the search bar to find cards by scene
number, or switch to Schedule mode where episodes are implicitly
separated by shoot day.

## 13.5 Episode and Scheduling

### 13.5.1 TV-format scene numbers in the one-liner

One-liner PDFs for TV productions often use `episode.scene` or
`episode/scene` notation (e.g. `1/27`, `2-05`, `01.14A`). Scene Cards
parses these and matches them against cards using the same episode and
scene number.

### 13.5.2 Matching across episodes in schedule

When a one-liner uses bare scene numbers without an episode prefix (as
is common on single-episode or film schedules), Scene Cards matches
each entry against all cards regardless of episode. Cards from episode 0
act as a wildcard — they match schedule entries with any or no episode
prefix.

Where the same scene number exists in more than one episode and the
one-liner doesn't specify the episode, Scene Cards will match the first
card it finds. Assign the card to the correct day manually (§9.5) if
the automatic match is wrong.

## 13.6 Episode in File Naming

Inside the document package, every card's media folder is prefixed with
its episode number:

```
Media/
├── thumbnails/
│   ├── Ep01_Scene_27.jpg
│   └── Ep02_Scene_5A.jpg
└── references/
    ├── Ep01_Scene_27/
    │   └── 001_storyboard.pdf
    └── Ep02_Scene_27/
        └── 001_location_photo.jpg
```

This means Scene 27 from Episode 1 and Scene 27 from Episode 2 each
have their own separate folder — no risk of mixing up media between
episodes that share a scene number.

Older documents written before the episode-aware build use plain
`Scene_N/` folders. Scene Cards reads both formats; all new writes use
the `EpNN_Scene_N` form.

## 13.7 Where to Go Next

- **Importing scripts** (including re-import and merge behaviour) —
  see §5.1.
- **Scheduling across episodes** — see §9.
- **Import Session Data across episodes** — matching uses the same
  episode-aware logic; see §12.4.
- **Document package layout** — see §4.8.
