<!--
TODO — still open for this chapter:
  1. Add the official support contact URL / email once established.
  2. Screenshots — the macOS About panel, the macOS Crash Reporter
     dialog, Console.app filtered to Scene Cards.
-->

# Chapter 21 — Diagnostics

Scene Cards has no built-in diagnostic export — there is no log file to
attach, no in-app "Report a Bug" button, and no hidden diagnostic mode.
This chapter covers what you *can* do when something goes wrong and you
need to investigate or contact support.

---

## 21.1 Finding Your App Version

Always include the app version when reporting an issue.

**🍎 macOS** — open **Scene Cards → About Scene Cards**. The panel shows
the version in the form `2026.X` and a build number below it.

**📐📱 iPadOS and iPhone** — the version is not shown inside the app.
Go to **Settings → Scene Cards**; the version and build number appear
at the top of the settings page.

---

## 21.2 Crash Reports

If Scene Cards crashes, the OS generates a crash report automatically.

### 🍎 macOS

After a crash, macOS may show the **Crash Reporter** dialog offering to
send a report to Apple. Allow it — Apple shares anonymised crash data
with developers via App Store Connect.

Crash logs are also written to disk:

1. Open **Finder → Go → Go to Folder…** (`⌘⇧G`).
2. Enter `~/Library/Logs/DiagnosticReports/`.
3. Look for files beginning with `Scene Cards` with a `.ips` extension,
   sorted by date.

To send a crash log to support, locate the most recent `.ips` file and
attach it to your support message.

### 📐📱 iPadOS and iPhone

Crash reports are uploaded to Apple automatically if you have opted in
to **Analytics & Improvements** in Settings → Privacy & Security →
Analytics & Improvements.

To share a crash report manually:

1. Go to **Settings → Privacy & Security → Analytics & Improvements →
   Analytics Data**.
2. Search for `SceneCards`.
3. Tap the report, then tap the share icon to send it.

---

## 21.3 Console Logs (🍎 macOS — Advanced)

Scene Cards writes diagnostic information to the system log during
operation — document loading strategies, import results, OCR decisions,
and similar runtime events. These are not persisted to a file; they
appear only in **Console.app** while the app is running.

To view live logs:

1. Open **Console.app** (in `/Applications/Utilities/`).
2. Select your Mac in the left sidebar under **Devices**.
3. In the search bar, enter `Scene Cards` and press Return.
4. Launch or operate Scene Cards — log messages appear in real time.

> ⓘ **Note** — Console shows logs from all processes. The volume can
> be high; use the **Action** menu → **Include Info Messages** and
> **Include Debug Messages** if messages are sparse.

This level of detail is useful for diagnosing import failures — for
example, to see exactly which pages were skipped during a PDF parse, or
which OCR path was taken for a one-liner.

---

## 21.4 Contacting Support

<!-- TODO: replace the placeholder below with the live support URL -->

If you can't resolve an issue using the troubleshooting steps in §19,
contact support at **[support contact — to be added]**.

When writing in, include:

- The app version and build number (§21.1).
- macOS, iPadOS, or iOS version.
- A description of what you were doing when the problem occurred.
- Any crash log (§21.2) or Console output (§21.3) if relevant.
- The document file if you are comfortable sharing it — right-click in
  Finder, choose **Compress**, and attach the resulting `.zip`.

---

## 21.5 Document Health Check

If a document behaves unexpectedly, inspect it directly:

1. Quit Scene Cards.
2. Right-click the document in Finder → **Show Package Contents**.
3. Open `payload.json` in a text editor and confirm it is valid JSON
   starting with `{`.
4. Check `Media/thumbnails/`, `Media/references/` and `Media/reports/`
   for any obviously corrupt or zero-byte files.

The three-strategy loading system (§18.9) means Scene Cards can often
recover from a partially corrupt `payload.json` automatically. If all
three strategies fail, Time Machine or iCloud Drive's version history
are the next resort (§20.2).

---

## 21.6 Where to Go Next

- **Troubleshooting by symptom** — §19.
- **Document package layout** — §18.8.
- **Format recovery strategies** — §18.9.
- **Backup and version history** — §20.2.
