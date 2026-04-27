<!--
TODO — still open for this chapter:
  1. Screenshots — the read-only banner, the OCR warning badge, the
     "Save Document First" alert, the Unmatched section in Schedule mode.
-->

# Chapter 19 — Troubleshooting

Problems are listed by symptom. If your issue isn't here, check the
relevant chapter or use the in-app **Quick Start** (`⌘⇧?`).

---

## Document

**The document won't open — "The file is corrupted"**

Scene Cards tries three recovery strategies before giving up (§18.9).
If it still fails:
1. Right-click the file in Finder and choose **Show Package Contents**.
2. Check that `payload.json` exists and is not empty.
3. Open `payload.json` in a text editor — it should be valid JSON
   starting with `{`.
4. If `payload.json` is missing or empty, check Time Machine or iCloud
   Drive's version history for an earlier copy.

**The document opens in read-only mode**

Your trial has ended or your subscription has lapsed. The banner at
the top of the wall shows **Read-only mode**. Tap or click
**Try free for 7 days** in the banner, or go to the App Store →
your account → Subscriptions to renew.

**"Save Document First" appears when creating a note or drawing**

Notes and drawings must be written into the document package, which
requires the document to have been saved at least once. Press `⌘S`
(🍎) or use the Files app save dialog (📐📱), then try again.

**Changes aren't being saved to iCloud**

Give iCloud a moment — sync is not instant. If the document still
hasn't appeared on the second device after a few minutes:
- Confirm both devices are signed into the same Apple ID.
- Check Settings → Apple ID → iCloud → iCloud Drive is enabled.
- On 📐📱 iPadOS and iPhone, check that Scene Cards is allowed iCloud
  access in Settings → Scene Cards.

---

## Script Import

**No cards appear after importing a script**

The most common cause is that the PDF is image-based (scanned) rather
than text-based, and Vision OCR could not extract scene headings. Try:
1. Check that your PDF is a proper text export from the screenwriting
   app, not a scan.
2. If it is a scan, allow a few extra seconds — OCR runs in the
   background and cards may appear after a short delay.
3. If still empty, open the PDF in Preview (🍎) or Files (📐📱) and
   confirm scene headings like `INT.` or `EXT.` are visible as
   selectable text, not images.

**Some scenes are missing after import**

Scene Cards looks for standard screenplay headings (`INT.`, `EXT.`,
`I/E.`). Scenes without a heading, or with a non-standard format,
will be skipped. Check the source PDF and correct the headings if
needed, then re-import (§5.1.2).

---

## Scheduling

**The schedule shows an orange OCR badge**

The one-liner PDF was image-based and Vision OCR was used to read it.
OCR is not 100% accurate — check the **Unmatched** section at the
bottom of Schedule mode (§9.4.4) and manually assign any cards that
landed in the wrong day (§9.5).

**Most cards land in "Unmatched"**

Scene Cards matches cards to schedule entries by scene number. If your
script uses a different numbering format from the one-liner, few will
match. Check:
- Do the scene numbers in the one-liner match those in the script?
- Is the one-liner using TV-format numbers (`1-14`) while the script
  uses film-format (`14`)? If so, the card's episode field may need
  to be set to match (§13.3).

---

## Sound Reports

**No entries appear on cards after importing a sound report**

Sound entries are matched to cards by scene number (§10.5). Check:
1. The sound report's scene numbers must match the cards' scene
   numbers. A mismatch of even one digit prevents a match.
2. Sound Devices filenames encode episode and scene in the leading
   digits — e.g. `1329S…` = ep 13, sc 29. If the card's episode or
   scene number differs, no match is made.
3. Confirm the report is Sound Devices PDF/CSV or Zaxcom Nomad format.
   Reports from other recorders may not be parsed (§10.2.1).

**Some sound report files are skipped in folder import**

Files that can't be matched to a shoot day are listed by name in the
summary alert at the end of the import. Attach them manually via the
day header **↓doc** button (§10.1.1).

---

## Reference Files

**A reference file won't open**

On 🍎 macOS, security-scoped bookmarks occasionally expire if the file
has been moved or the volume remounted. Open the inspector, navigate to
the file in the carousel, and tap **Open in App** — if it fails, remove
the reference (§8.5) and re-add the file from its new location.

**Dropped files disappear after closing the app**

If the document has not been saved, dropped reference files are held
in memory only. Save the document (`⌘S`) before closing, or save
immediately after dropping files.

---

## Printing

**The printout is blank or shows the wrong content**

Printing always uses the **Scenes mode** wall, regardless of which
mode you're in when you press `⌘P`. Switch to Scenes mode (`⌘⇧1`)
first, then print.

**Cards are very small on the printed page**

The layout is fixed at 2 columns × 3 rows per A4 page (§11.1.3). If
you have many cards, they will be small — this is expected. There is
no option to change the grid size in the current version.

---

## Subscription and Trial

**"Import Session Data" / import commands are greyed out**

These require an active subscription or trial. If your trial has
expired, the read-only banner appears. Renew via the App Store.

**Restored a subscription but the app still shows read-only**

Force-quit Scene Cards and relaunch — the subscription check runs on
launch and will pick up the restored entitlement.

**Purchased on one device, want to use on another**

Sign in to the same Apple ID on the second device. Launch Scene Cards
— it checks your App Store entitlements automatically and unlocks
without any further steps.
