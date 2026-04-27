<!--
TODO — still open for this chapter:
  1. Screenshots — the macOS Settings window (General tab, Printing tab).
  2. RESOLVED — macOS has no in-app "Manage Subscription" route.
     The button only exists in the iOS ⋯ overflow menu (UIApplication
     itms-apps deep-link). macOS users must go via App Store → account
     icon → Subscriptions. §17.3 is accurate as written.
-->

# Chapter 17 — Settings and Preferences

Scene Cards has a small set of app-wide preferences. On 🍎 macOS they
live in the Settings window; on 📐📱 iPadOS and iPhone there is no
separate settings panel — the only in-app option is subscription
management in the ⋯ overflow menu.

## 17.1 🍎 macOS — Settings Window

Open with `⌘,` or `Scene Cards → Settings…`.

### General

| Setting | Default | What it does |
|---|---|---|
| Open inspector automatically when selecting a tile | On | Inspector opens whenever you click a card. Turn off to open it manually. |
| Confirm before deleting a tile | On | Shows an alert before deleting a card. Turn off if you find the confirmation slow. |
| Large scene numbers on tiles | On | Displays the scene number prominently on each card face. |

### Printing

No configurable options. This tab confirms that printing is always A4
portrait with no margins and that cards scale automatically to fit the
page. See §11 for the full printing guide.

## 17.2 Document-Level Preferences

Some preferences belong to the document rather than the app — they
travel with the `.scenecards` file and apply only to that production.

| Preference | Where to change it |
|---|---|
| Wall width (columns) | 📐📱 Pinch on the wall to adjust (1–10 columns) |
| Character colours | Inspector → a card with character dialogue → colour picker |
| Excluded characters | Inspector → character list → exclude toggle |

## 17.3 Subscription Management

**📐📱 iPadOS and iPhone** — tap **⋯ → Manage Subscription…** to open
the App Store subscriptions page, where you can renew, cancel or change
your plan. If the trial has expired, **⋯ → Try Scene Cards Pro Free for
7 Days…** restarts the paywall flow.

**🍎 macOS** — manage your subscription through the App Store app:
open App Store → click your account icon → Subscriptions.

> ⓘ **Note** — restoring a subscription purchased on another device:
> open the App Store and sign in with the same Apple ID. Scene Cards
> checks your entitlements automatically on launch.
