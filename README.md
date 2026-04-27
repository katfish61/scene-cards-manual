# Scene Cards — Operations Manual

Working source for the Scene Cards operations manual. One chapter per file,
edited in-place as the app evolves. Final delivery format (PDF, DocC, on-device
help bundle) is decided later — markdown is the working medium.

## Layout

```
Docs/Manual/
├── README.md                      ← you are here
├── 00-FrontMatter.md              (TBD)
├── 01-Introduction.md             ← drafted
├── 02-QuickStart.md               ← drafted
├── 03-Orientation.md              ← drafted
├── 04-DocumentsAndFiles.md        ← drafted
├── 05-BuildingTheWall.md          ← drafted
├── 06-WorkingWithScenes.md        ← drafted
├── 07-StillsAndThumbnails.md      ← drafted
├── 08-ReferenceFiles.md           ← drafted
├── 09-Scheduling.md               ← drafted
├── 10-ShootReports.md             ← drafted
├── 11-PrintingAndExport.md        ← drafted
├── 12-ImportSessionData.md        ← drafted
├── 13-MultiEpisode.md             ← drafted
├── 14-Collaborating.md            ← drafted
├── 15-ToolbarAndMenuReference.md  ← drafted
├── 16-KeyboardShortcuts.md        ← drafted
├── 17-SettingsAndPreferences.md   ← drafted
├── 18-FileFormatSpec.md           ← drafted
├── 19-Troubleshooting.md          ← drafted
├── 20-Maintenance.md              ← drafted
├── 21-Diagnostics.md              ← drafted
├── Appendix-A-SupportedFileFormats.md  ← drafted
├── Appendix-B-Glossary.md         ← drafted
├── Appendix-C-SampleWorkflows.md  ← drafted
├── Appendix-D-Changelog.md        ← drafted
└── assets/                        (screenshots, diagrams)
```

## House Style

These conventions apply across every chapter. When drafting, follow them so the
final book reads as one document, not twenty-odd.

### Voice

- **Task-first, not feature-first.** Headings describe what the reader is
  doing ("Import a Sound Report") rather than naming a UI surface ("The Sound
  Import Dialog").
- **Short, declarative sentences.** Assume the reader is on set and in a
  hurry.
- **No marketing.** No "powerful", "seamless", "effortless". State what it
  does.
- **Second person, active voice.** "Tap Import" rather than "The user should
  tap Import".

### Structure within a chapter

1. One-paragraph orientation — what this chapter covers and who it's for.
2. Numbered subsections (`## 1.1`, `## 1.2`, …) mirroring the manual ToC.
3. Procedures as numbered lists; concepts as prose.
4. Close with **Where to Go Next** cross-references when useful.

### Platform badges

Prefix headings with the relevant badge(s) when behaviour differs by platform:

- 🍎 macOS
- 📐 iPadOS
- 📱 iPhone

Use `📐📱` when behaviour is identical on iPadOS and iPhone. Omit badges
entirely when the procedure is identical across all three platforms.

### Callouts

Use the same four callouts everywhere. One type per block — don't stack.

```markdown
> ⓘ **Note** — supplementary information.

> ✱ **Tip** — shortcut or best practice.

> ⚠ **Caution** — risk of data loss or wasted time.

> 🔒 **Permission required** — triggers a system permission prompt.
```

### Keyboard notation

Modifier keys use Apple symbols: ⌘ ⌥ ⌃ ⇧. Combinations have no separator:
`⌘S`, `⌥⌘I`.

### Menu paths

`File → New`, `Edit → Undo`, `View → Show Inspector`.

### Screenshots

Screenshots live in `Docs/Manual/images/`. Naming convention:

- `C{chapter}_{section}.png` — one image for a section, e.g. `C3_1.png` for §3.1
- `C{chapter}_{section}a.png`, `…b.png` — multiple images in the same section
- Sub-sections: `C9_4_1.png` for §9.4.1

Reference in markdown as `![Alt text](images/C3_1.png)`.

### Placeholder filenames

Use `MyProduction.scenecards` for document examples and `Ep01_Scene_5` for
scene-folder examples unless the chapter requires otherwise.

### Terminology

- **Card** — the user-facing term for a single scene on the wall. Always use
  this in the manual.
- **Tile** — an internal / developer term used in the codebase
  (`TileThumbnailView`, `Tile.swift`, etc.). Avoid in user-facing text.
- **Wall** — the grid that holds the cards.
- **Slot** — a position on the wall; a card occupies one slot.

### Cross-references

Link inline as `see §10.3`, `see Appendix B`. Chapter titles only appear at
first mention; after that use the section number.

## Working with Claude Code on this

| You want to… | Say… |
|---|---|
| Have Claude re-read your edits | "re-read chapter 1" |
| Apply a specific edit | "in §1.2 drop the UPM row — it's redundant" |
| Draft the next chapter | "draft chapter 2" |
| Fix a confirmed fact globally | "min macOS is 14.0, update everywhere" |
| Regenerate a section | "rewrite §1.7 as Option B only" |

## Resolved Facts

Canonical answers that now apply across the whole manual. Do not re-ask.

- **Platforms:** macOS, iPadOS, and iPhone.
- **Minimum OS:** macOS 13.5 (Ventura); iPadOS 16.6; iOS 16.6.
- **Monetisation:** annual subscription with 7-day free trial. No free
  tier — the trial gives full access to everything; after expiry the
  document opens read-only. Never write "free version" or "free tier".
- **iCloud sync:** implemented — iCloud Documents capability added
  (container iCloud.com.keithtunney.scenecards, CloudDocuments service).
  File-level sync via iCloud Drive; not real-time multiplayer.
- **App Store status:** live on Mac App Store, iPadOS App Store, and iOS App Store.
- **Default wall width:** 8 cards on macOS, 6 cards on iPadOS, 3 cards on iPhone (portrait).
- **User-facing term:** *card*. *Tile* is internal only.

## Open Questions

Queries that need a human answer before drafting can go below. Clear them as
they're resolved.

- [ ] Does the iPadOS Welcome screen re-appear on demand, and where from?
  Affects §1.6.2 tip.
- [ ] Ship a sample `PaperEdit-Demo.pdf` in `Docs/Manual/assets/` so Quick
  Start readers have a script to try immediately. Affects §2.

## Content Parked for Later Chapters

Researched material that belongs in a future chapter. Move it in and delete
from here once the target chapter is drafted.

*(Nothing parked — the §5.1 re-import block has landed in
`05-BuildingTheWall.md` §5.1.2.)*
