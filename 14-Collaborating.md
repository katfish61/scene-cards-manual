<!--
TODO — still open for this chapter:
  1. Screenshots — the Files app showing a .scenecards document in
     the iCloud Drive / Scene Cards folder, an AirDrop send in progress.
  2. RESOLVED — iCloud Documents sync was added in commit a746bab:
     entitlements now include icloud-container-identifiers and
     icloud-services (CloudDocuments); NSUbiquitousContainers added
     to Info.plist with container iCloud.com.keithtunney.scenecards.
     §14.3 updated with full iCloud Drive section.
-->

# Chapter 14 — Collaborating

Scene Cards is a document-based app — collaboration happens by passing
the document file between people. There is no real-time multiplayer
editing; instead, you share the `.scenecards` package, each person
works on their copy, and changes are merged back using Import Session
Data (§12). iCloud Drive keeps your document in sync across your own
devices automatically. This chapter covers iCloud Drive, sharing a
document with others, and the merge workflow.

## 14.1 iCloud Drive

Scene Cards stores documents in iCloud Drive so they are available on
every Mac and iPad signed into the same Apple ID. Save once on one
device — the file appears on the others automatically.

> ⓘ **Note** — iCloud Drive sync requires an active subscription or
> free trial. In read-only mode the document still opens from iCloud
> Drive, but you cannot edit it until a subscription is active.

### 14.1.1 Where documents live in iCloud

On both platforms, Scene Cards documents appear under
**iCloud Drive → Scene Cards** in the Files app (📐 iPadOS) or in
Finder's iCloud Drive section (🍎 macOS). You can create subfolders
there to organise productions.

### 14.1.2 Keeping two devices in sync

When you edit a document on one device and save, iCloud uploads the
changes. The updated file downloads to your other devices in the
background. Open the document there and it picks up where you left
off.

> ⚠ **Caution** — iCloud sync is file-level, not real-time. If you
> open the same document on two devices at the same time and both save,
> iCloud may keep one version and create a duplicate of the other.
> Work on one device at a time, or use Import Session Data (§12) to
> reconcile diverged copies.

### 14.1.3 Downloading a document on a new device

If a document shows a cloud icon (📐 iPadOS) or a download indicator
(🍎 macOS) it has not yet downloaded to that device. Tap or double-click
it to trigger the download before opening.

## 14.2 Sharing a Document With Others

A `.scenecards` package is self-contained — every still, reference file
and report is copied inside the bundle. You can hand the whole thing to
a collaborator by any means that transfers a file.

### 14.2.1 AirDrop

**📐 iPadOS**
1. Open the Files app and locate the document.
2. Long-press the file and tap **Share**.
3. Choose the recipient in the AirDrop sheet.

**🍎 macOS**
1. In Finder, right-click the `.scenecards` file.
2. Choose **Share → AirDrop** and select the recipient.

The recipient opens the file directly in Scene Cards once it arrives.

### 14.2.2 Cloud storage (Dropbox, Google Drive, etc.)

Place the `.scenecards` file in any shared cloud folder accessible to
both parties. Only one person should edit at a time — the last save
wins if two people save simultaneously.

> ⚠ **Caution** — agree on a hand-off process: one editor finishes
> and saves, then the other opens the updated file.

### 14.2.3 Email and Messages

Attach the `.scenecards` file to an email or message. For large
productions with many reference files the package can be several
hundred megabytes — check the recipient's attachment limit first, or
use a cloud or AirDrop link instead.

## 14.3 The Async Merge Workflow

When two people have worked on separate copies of the same document,
use **Import Session Data** (§12) to bring one person's work into the
other's. You choose exactly what to merge — thumbnails, reference
files, shoot reports, schedule data — and leave the rest untouched.

A typical two-person workflow:

1. Editor A creates the main document and shares it with Editor B
   (AirDrop, cloud storage, or by both opening the same shared folder).
2. Editor B works on their copy — adding references, importing reports,
   adjusting the schedule.
3. Editor B shares their updated document back to Editor A.
4. Editor A opens `File → Import Session Data…` (🍎 macOS, §12),
   selects Editor B's document, and picks what to bring across.
5. The result is Editor A's document with Editor B's additions merged
   in, overwriting only the categories chosen.

> ✱ **Tip** — Import Session Data is one-directional: you pull from a
> source into your current document. If both parties have made changes
> you want to keep, run the import in both directions, or agree that
> one document is the authoritative copy before work starts.

## 14.4 What Isn't Supported

**Real-time simultaneous editing** — iCloud Drive sync is file-level.
There is no multiplayer editing where two people see each other's
changes live.

**Apple Handoff** — picking up mid-session on a different device is
not supported in the current version. Open the document fresh on the
second device after iCloud has synced.

**Automatic conflict resolution** — if the same document is edited on
two devices simultaneously and both save, iCloud handles the conflict
at the file level (keeping one version and renaming the other). Scene
Cards has no built-in conflict UI — use Import Session Data to
reconcile diverged copies manually.

## 14.5 Where to Go Next

- **Import Session Data** — the full merge workflow is in §12.
- **Shoot reports** — importing reports from a day-file into the main
  document is a common collaboration use case; see §10.6.
- **Document package layout** — understanding what's inside the
  package helps when diagnosing sync issues; see §4.8.
