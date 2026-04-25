<!--
TODO — still open for this chapter:
  1. Screenshots — Show Package Contents in Finder, the Media/ folder
     open in Finder.
-->

# Chapter 20 — Maintenance

Day-to-day use of Scene Cards requires little housekeeping. This
chapter covers the tasks worth doing occasionally: reclaiming disk
space, backing up your documents, and keeping the app current.

---

## 20.1 Reclaiming Disk Space

A `.scenecards` document grows over time as you add reference files,
stills, and shoot reports. Scene Cards never deletes files from the
`Media/` folder automatically — this is intentional, so you can always
recover content by browsing the package directly.

When a document gets large, use Finder to remove what you no longer
need.

**How to open the package in Finder:**

1. Right-click the document in Finder.
2. Choose **Show Package Contents**.
3. Navigate to `Media/` and delete the folders or files you want to
   remove.

> ⚠ **Caution** — deletions made in Finder are permanent and cannot
> be undone inside Scene Cards. Close the document in Scene Cards
> before deleting, or save immediately after to ensure the package is
> consistent.

### 20.1.1 Thumbnails

Thumbnails live in `Media/thumbnails/`. One file per card, named
`Ep{NN}_Scene_{N}.jpg` (or `.png`).

**Thumbnails are deleted automatically** when a card is deleted inside
Scene Cards. Orphaned thumbnail files are unlikely; you rarely need to
clean this folder by hand.

### 20.1.2 Reference Files

Reference files live in `Media/references/`, one subfolder per card
(§8.7). These folders are **not deleted** when a card is deleted.
After removing cards — including during a script re-import that drops
scenes — their reference folders remain.

To reclaim space:
1. Open the package in Finder as above.
2. In `Media/references/`, identify folders whose scene numbers no
   longer exist on the wall.
3. Delete those folders.

### 20.1.3 Report Files

Report files live in `Media/reports/` (§10.7). Removing a report
badge from a day header inside Scene Cards deletes the attachment
record but leaves the file on disk.

To reclaim space:
1. Open the package in Finder.
2. In `Media/reports/`, locate the day folder and delete the specific
   report file you no longer need.

> ⓘ **Note** — re-importing a corrected report does not overwrite the
> old file; it writes alongside it. If you re-import frequently,
> `Media/reports/` can accumulate superseded copies.

---

## 20.2 Backing Up

Scene Cards documents are standard files and work with any backup
strategy you already use.

### 🍎 Time Machine

Time Machine backs up `.scenecards` packages automatically along with
the rest of your Mac. Because the package is a directory bundle, Time
Machine versions individual files within it — you can restore a single
thumbnail or the entire document from any snapshot.

To restore a previous version:
1. Open Time Machine with the document window in focus.
2. Navigate to the snapshot you want.
3. Click **Restore** to recover the whole package, or drill into
   **Show Package Contents** in the Time Machine browser to recover a
   specific file.

### iCloud Drive

If iCloud Drive is enabled (§14.1), your document syncs to iCloud
automatically and is accessible on all devices signed in to the same
Apple ID. iCloud Drive also keeps deleted files in the **Recently
Deleted** folder in iCloud.com for 30 days.

To check available iCloud storage:
- **🍎 macOS** — System Settings → Apple ID → iCloud → Manage.
- **📐 iPadOS** — Settings → Apple ID → iCloud → Manage Account Storage.

### Manual Archive

For a production archive at wrap, duplicate the document in Finder
(`⌥`-drag on 🍎, or long-press → Duplicate on 📐), rename the copy
with a date stamp, and store it alongside your other deliverables.

---

## 20.3 App Updates

Scene Cards is distributed through the Mac App Store and iPadOS App
Store. There is no in-app update mechanism — updates arrive through
the App Store app.

To check for updates:
- **🍎 macOS** — open the App Store → **Updates** tab.
- **📐 iPadOS** — open the App Store → your account → **Updates**.

Enable automatic updates in System Settings → App Store (🍎) or
Settings → App Store (📐) to receive updates without prompting.

> ⓘ **Note** — Scene Cards opens older document formats automatically
> with no conversion step required (§18.9). Updating the app is safe;
> existing documents are not modified until you save them in the new
> version.

---

## 20.4 Where to Go Next

- **Reference file locations** — §8.7.
- **Report file locations** — §10.7.
- **iCloud sync setup** — §14.1.
- **Document package layout** — §18.8.
- **Format compatibility and recovery** — §18.9.
- **Recovery from a corrupted document** — §19, "The document won't
  open".
