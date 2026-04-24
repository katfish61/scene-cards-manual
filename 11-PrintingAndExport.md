<!--
TODO — still open for this chapter:
  1. Screenshots — the printed page layout (2×3 grid, card content),
     the macOS print dialog, the iPadOS print sheet.
  2. RESOLVED — omitted cards appear on the printed wall. The scene
     number field renders as e.g. "02 / 15A OMITTED". §11.1.2 updated.
-->

# Chapter 11 — Printing

Scene Cards can print the scene wall as a grid of cards — one job
produces a series of A4 portrait pages, six cards per page, in slot
order. The printout is useful for pinning to a physical wall, sharing
with crew, or sending as a PDF. This chapter covers starting a print
job, what appears on each card, saving to PDF, and what cannot be
printed in the current version.

## 11.1 Printing the Wall

### 11.1.1 Starting a print job

Three routes reach the print dialog:

| Route | Action |
|---|---|
| Menu | `File → Print Wall Layout…` |
| Keyboard | `⌘P` |
| 📐 iPadOS toolbar | **⋯** → **Print…** |

Both platforms open the standard system print dialog — macOS shows the
native print panel; iPadOS shows the print sheet. From there, choose a
printer, set the number of copies, and print.

### 11.1.2 What each card shows

Each printed card contains, from top to bottom:

| Element | Notes |
|---|---|
| Scene number | Episode and scene (e.g. `02 / 15`, `02 / 15A OMITTED`) — omitted cards print with their OMITTED label |
| Brief | One-line description; falls back to the full description if no brief is set |
| Still image | Up to half the card height; omitted if no still has been attached |
| Comments | Shown in smaller text below the image |

Card borders are rounded. The background is white. There is no colour
coding in the current print layout — revision colours and badge icons
do not appear.

### 11.1.3 Page layout

The layout is fixed:

- **Paper size:** A4 portrait (210 × 297 mm)
- **Grid:** 2 columns × 3 rows = **6 cards per page**
- **Order:** Wall slot order (the same left-to-right, top-to-bottom
  order you see in Scenes mode)
- **Margins:** None — the grid runs to the printable area edge

There are no configurable layout options in the current version — column
count, card size and paper size are all fixed.

### 11.1.4 Which mode to be in

The print job always uses the **Scenes mode wall grid**. Switch to
Scenes mode (`⌘⇧1`) before printing.

> ⓘ **Note** — Schedule mode and Locations mode are not printable in the
> current version. The print command is available from any mode, but the
> output is always the Scenes wall. To print a shoot schedule, print
> the one-liner PDF directly from its source app.

## 11.2 Saving to PDF

There is no dedicated "Export PDF" command. Use the system print dialog
instead:

**🍎 macOS** — in the print dialog, click the **PDF** pop-up menu at the
bottom-left and choose **Save as PDF…**. Name the file and save.

**📐 iPadOS** — in the print sheet, pinch to zoom the preview — this
converts the job to a PDF in a preview sheet. Tap the share button (⬆)
to save to Files, send by AirDrop, or attach to an email.

The resulting PDF is a faithful reproduction of the printed layout —
six cards per A4 page, in slot order.

## 11.3 Where to Go Next

- **Sharing the document itself** — the `.scenecards` package can be
  shared directly from the Files app (📐 iPadOS) or Finder (🍎 macOS).
  See §4.7.
- **Reference files** — stills and documents attached to cards do not
  appear on the printed wall. To share them, use the share sheet in the
  inspector (§8.4.4).
- **Import Session Data** — to hand off a wall to a colleague as a
  Scene Cards document, see §12.
