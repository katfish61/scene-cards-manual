<!--
TODO — still open for this chapter:
  1. Screenshots — Cloud Walls sheet, Sync & Account sign-in screen,
     invitation acceptance dialog. Save under Docs/Manual/assets/.
-->

# Chapter 14 — Collaborating

Scene Cards supports two collaboration modes:

- **Cloud Walls** — real-time sync via the internet. All platforms (macOS, iOS, Android) share one live wall. Anyone with access sees changes as they happen.
- **Document hand-off** — pass the `.scenecards` file between people by AirDrop, iCloud Drive, cloud storage, or email. Changes are merged using Import Project Data (§12).

This chapter covers Cloud Walls first, then the file-based workflow for offline or iCloud-only setups.

---

## 14.1 Cloud Walls — Real-time sync

Cloud Walls keeps one wall in sync across every device on your team — Mac, iPhone, iPad, and Android — in real time, over the internet.

### 14.1.1 What you need

- An internet connection on each device
- A Scene Cards account (free — see §14.1.2)
- The current version of Scene Cards on every device

You do **not** need a Google or Gmail account. Scene Cards can sign you in with any email address.

### 14.1.2 Signing in

Open the **"Sync & Account…"** sheet:

- **macOS**: click the cloud icon (☁) in the toolbar → "Sync & Account…"
- **iOS/iPadOS**: tap the cloud icon in the toolbar → "Sync & Account…"
- **Android**: tap the cloud icon in the toolbar → "Sync & Account…"

You'll see two sign-in options:

**Option A — Sign in with any email (no Google account needed)**

1. Under "Sign in with any email", type your email address. Any email works — iCloud, Outlook, Yahoo, a work address, anything.
2. Tap **"Send sign-in link"**.
3. Open your email on the **same device** — you'll have a message from Scene Cards.
4. Tap the link in the email. Scene Cards opens and you're signed in.

> ⓘ **Same device** — the magic link is designed to be tapped on the same phone, tablet, or Mac where Scene Cards is running. If you open the email on a different device first, Scene Cards will ask you to type your email address again to confirm — just enter the same address.

**Option B — Sign in with Google**

Tap **"Sign in with Google"** and choose your account. Requires a Google/Gmail account.

> ✱ **Android tip** — most Android phones already have a Google account configured for the Play Store, so "Sign in with Google" is usually the fastest option on Android.

Once signed in, Scene Cards remembers you. You won't be asked again on the same device unless you sign out.

### 14.1.3 Setting up a production (the owner does this)

One person — whoever manages the wall — creates the **production** that the whole team shares. Do this immediately after signing in.

1. In "Sync & Account…", tap **"Create Production"**.
2. Give it a name (e.g. "Pilot 2026" or "Feature — Aug Shoot").
3. Tap "Create". You're now the production owner.

A production is a named workspace. All your Cloud Walls and team members sit inside it.

### 14.1.4 Inviting crew

The production owner invites everyone else by email.

1. In "Sync & Account…", find the **"Invite by email"** field.
2. Type a crew member's email address exactly as they'll use to sign in.
3. Tap **"Invite"**. They receive an invitation email.
4. Repeat for each person.

> ⚠ **Use the same address** — when you invite someone, they must sign in with exactly that email address (or a Google account whose address matches). If they sign in with a different address, the invitation won't be automatically applied.

### 14.1.5 Accepting an invitation (crew members)

When a crew member signs in for the first time after being invited, Scene Cards finds the pending invitation automatically and shows an "Accept / Decline" prompt. They tap **"Accept"** and immediately have access to the production's walls.

If the prompt doesn't appear, ask them to:
1. Make sure they signed in with the exact email you invited.
2. Pull down to refresh in "Sync & Account…" or close and reopen the sheet.

### 14.1.6 Opening a shared wall

After accepting the invitation, crew members tap **"Cloud Walls"** in the toolbar to see all walls in the production. Tap any wall to open it. Changes made by anyone on the team sync within seconds.

### 14.1.7 Step-by-step: first-time setup for a mixed team

Below is a complete worked example for a common scenario: one owner on macOS/iOS, two crew on iOS, one on Android, with a mix of Google and non-Google accounts.

**Before you begin** — everyone downloads Scene Cards:
- macOS and iOS: App Store
- Android: Google Play

**The owner (macOS + iOS, no Gmail):**

1. Open Scene Cards on Mac.
2. Click the cloud icon → "Sync & Account…".
3. Under "Sign in with any email", type your email (iCloud, Outlook, etc.) → "Send sign-in link".
4. Open your email, tap the link — you're signed in.
5. Tap "Create Production" → name it → "Create".
6. In the "Invite by email" field, invite each crew member one at a time.

**Crew member A — iPhone, has Gmail:**

1. Open Scene Cards on iPhone.
2. Tap the cloud icon → "Sync & Account…".
3. Tap "Sign in with Google" → select their Gmail account.
4. Tap "Accept" on the invitation prompt.

**Crew member B — iPhone, no Gmail:**

1. Open Scene Cards on iPhone.
2. Tap cloud icon → "Sync & Account…".
3. Under "Sign in with any email", type their email → "Send sign-in link".
4. Open their email app on the same iPhone — tap the link.
5. Tap "Accept" on the invitation prompt.

**Crew member C — Android:**

1. Open Scene Cards on Android — it works immediately in local mode.
2. Tap the account icon in the top bar.
3. **Fastest:** tap "Sign in with Google" → select their Google account (Android phones nearly always have one for the Play Store).
   **Or:** type their email → "Send sign-in link" → open email → tap link.
4. Tap "Accept" on the invitation prompt.

**Everyone is now connected.** Tap "Cloud Walls" on any device to open the shared wall.

### 14.1.8 What syncs

| Item | Syncs in real time |
|------|-------------------|
| Scene cards (brief, location, comments, revision colour, omit status) | Yes |
| Still images and reference files | Yes (uploaded on add, downloaded on open) |
| Shoot reports | Yes |
| Episode titles and wall grid layout | Yes |
| Local `.scenecards` file on disk | No — Cloud Walls is a separate copy |

> ⓘ **Local vs. cloud** — a Cloud Wall lives in the cloud. Your local `.scenecards` documents (in iCloud Drive or on-device) are separate. You can work locally without a cloud account; signing in and creating a Cloud Wall doesn't move your local documents.

### 14.1.9 Switching productions

If you belong to more than one production (e.g. you worked on two shows), use "Sync & Account…" → "Switch" to change the active production. Only walls from the active production appear in Cloud Walls.

### 14.1.10 Signing out

"Sync & Account…" → "Sign Out". Your local walls are not affected. Cloud Walls become inaccessible until you sign in again.

---

## 14.2 iCloud Drive — your own devices

iCloud Drive keeps your local `.scenecards` documents in sync across all your own Macs and iOS devices automatically — no account beyond your Apple ID required.

### 14.2.1 Where documents live

Documents appear under **iCloud Drive → Scene Cards** in the Files app (iOS/iPadOS) or in Finder's iCloud Drive section (macOS). Create subfolders there to organise productions.

### 14.2.2 Keeping devices in sync

Edit on one device and save — iCloud uploads the change. The updated file downloads to your other devices in the background. Open it there and it picks up where you left off.

> ⚠ **One editor at a time** — iCloud sync is file-level, not real-time. If two devices edit the same document simultaneously and both save, iCloud may keep one version and create a duplicate. Work on one device at a time, or use Import Project Data (§12) to reconcile diverged copies. For multi-person collaboration, Cloud Walls (§14.1) is the better choice.

### 14.2.3 Downloading a document on a new device

If a document shows a cloud icon (iOS) or download indicator (macOS) it hasn't downloaded yet. Tap or double-click it to trigger the download before opening.

---

## 14.3 Document hand-off

A `.scenecards` package is self-contained — every still, reference file and report lives inside the bundle. Hand it to anyone by any means that transfers a file.

### 14.3.1 AirDrop

**macOS:** Finder → right-click the `.scenecards` file → Share → AirDrop → select recipient.

**iOS/iPadOS:** Files app → long-press the file → Share → AirDrop → select recipient.

The recipient opens the file directly in Scene Cards once it arrives.

### 14.3.2 Cloud storage (Dropbox, Google Drive, etc.)

Place the `.scenecards` file in a shared folder accessible to both parties. Agree on a hand-off process: one editor finishes and saves, then the other opens the updated file. The last save wins if two people save simultaneously.

### 14.3.3 Email and Messages

Attach the `.scenecards` file to an email or message. Large productions with many reference files can be several hundred megabytes — use AirDrop or cloud storage for those.

### 14.3.4 Merging work from two copies

When two people have worked on separate copies of the same document, use **Import Project Data** (§12) to bring one person's work into the other's. You choose exactly what to merge.

A typical two-person workflow:

1. Person A creates the main document and shares it with Person B.
2. Person B adds references, reports, and schedule data on their copy.
3. Person B shares their updated document back to Person A.
4. Person A opens **File → Import Project Data…** (macOS, §12), selects Person B's document, and picks what to bring across.

See §12 for the full details.

---

## 14.4 What isn't supported

**Real-time simultaneous editing of local documents** — iCloud Drive sync is file-level. For real-time collaboration, use Cloud Walls (§14.1).

**Apple Handoff** — picking up mid-session on a different device is not supported. Open the document fresh on the second device after iCloud has synced.

**Automatic conflict resolution for local documents** — if two devices edit the same `.scenecards` file simultaneously, the file system handles it (usually keeping one version and creating a duplicate). Use Import Project Data (§12) to reconcile manually.

---

## 14.5 Where to go next

- **Cloud Walls in depth** — once the wall is open, everything about building and editing it is the same as a local wall; start at §5.
- **Import Project Data** — the full merge workflow for local documents is in §12.
- **Shoot reports** — a common collaboration use case is importing a day-file into the main document; see §10.6.
- **Document package layout** — understanding what's inside the package helps when diagnosing sync issues; see §4.8.
