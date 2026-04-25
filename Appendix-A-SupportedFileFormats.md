<!--
TODO — still open for this appendix:
  1. Screenshots — not required; this is a reference table.
-->

# Appendix A — Supported File Formats

This appendix lists every file format Scene Cards can read or write,
organised by task. For step-by-step import procedures see the
relevant chapter.

---

## A.1 Files You Import Into Scene Cards

### Scripts

| Format | Extension | What is extracted |
|---|---|---|
| PDF (text-based) | `.pdf` | Scene headings, scene numbers, location sluglines, action/dialogue text, revision colour |
| FDX (Final Draft) | `.fdx` | Scene headings, scene numbers, location sluglines, revision colour |

Both formats are accepted by the same importer (§5.1). The PDF must be
a proper text export from a screenwriting application — a scanned PDF
will not yield scene headings (§5.1.1).

Revision colours are detected from the PDF page colour or the FDX
revision attribute and mapped to standard names (`goldenrod`, `blue`,
`pink`, `green`, etc.).

### One-Liner / Schedule

| Format | Extension | Notes |
|---|---|---|
| PDF (text-based or image-based) | `.pdf` | Text extraction via PDFKit; Vision OCR fallback for image-based PDFs |

Scene Cards accepts PDFs produced by Movie Magic Scheduling, EP
Scheduling, and similar strip-board applications. If the PDF is
image-rendered (vector output that cannot be selected as text), Vision
OCR runs automatically and an orange badge appears in Schedule mode
(§9.4.4).

See §9.1 for the import procedure.

### Sound Reports

Scene Cards parses sound reports from two recorder families. Reports
from other recorders can be attached to a shoot day as unread files
(§10.1).

| Recorder | Format | Extension | How scenes are matched |
|---|---|---|---|
| Sound Devices | PDF | `.pdf` | Episode and scene encoded in filename: `{ep}{scene}S{slate}T{take}` e.g. `1329S142T01` |
| Sound Devices | CSV | `.csv` | Scene column in the export table |
| Zaxcom Nomad | PDF | `.pdf` | Scene and take encoded in filename: `{scene}T{take}` e.g. `27T002` |

**Wild tracks** (Sound Devices): filename pattern `{ep}{scene}WTT{take}`,
e.g. `447WTT01` = ep 4, scene 47.

**Wild tracks** (Zaxcom): filename pattern `{scene}TWT{n}`,
e.g. `30TWT1`.

See §10.2 for the import procedure and §10.5 for the matching logic.

### Camera and Continuity Reports

Camera and continuity PDFs are accepted as **attach-only** files — they
are stored in the document package (§18.8) and can be opened from the
Schedule day header, but their contents are not parsed into card data.

| Type | Format | Extension |
|---|---|---|
| Camera report | PDF | `.pdf` |
| Continuity sheet | PDF | `.pdf` |

See §10.3 for attaching these reports.

### Day-Level Documents

Call sheets and production essentials are also attach-only.

| Type | Format | Extension |
|---|---|---|
| Call sheet | PDF | `.pdf` |
| Essentials | PDF | `.pdf` |

See §10.4 for attaching these documents.

### Images

Images are used for hero stills (§7) and as reference files (§8).

| Format | Extension(s) | Used for |
|---|---|---|
| JPEG | `.jpg` `.jpeg` | Hero stills, references |
| PNG | `.png` | Hero stills, references |
| HEIC / HEIF | `.heic` `.heif` | Hero stills, references |
| TIFF | `.tiff` `.tif` | Hero stills, references |
| GIF | `.gif` | References |
| WebP | `.webp` | References |
| BMP | `.bmp` | References |
| RAW (Canon) | `.cr2` | References |
| RAW (Nikon) | `.nef` | References |
| RAW (Sony) | `.arw` | References |
| RAW (generic) | `.raw` | References |

> ⓘ **Note** — RAW formats can be attached as reference files and
> previewed via Quick Look on macOS, but Scene Cards generates the
> thumbnail from the JPEG preview embedded in the RAW file, not from
> the raw sensor data.

### Reference Files

Reference files (§8) accept a broad range of types. The file picker
filters to common categories, but any file the OS can handle can be
added by dragging it directly onto the carousel.

| Category | Common formats |
|---|---|
| Images | See Images table above |
| Documents | PDF, Word (`.docx`), Pages, RTF, plain text, Markdown |
| Spreadsheets | Excel (`.xlsx`), Numbers, CSV |
| Presentations | PowerPoint (`.pptx`), Keynote |
| Video | MP4, MOV, M4V |
| Audio | MP3, M4A, AAC, WAV, AIFF |
| Folders | Any folder — copied as a subfolder into the card's reference folder |

Files are stored verbatim in `Media/references/` (§8.7); Scene Cards
does not transcode or alter them.

---

## A.2 Files Scene Cards Produces

| Output | Format | Notes |
|---|---|---|
| Document | `.scenecards` package | FileWrapper directory; contains `payload.json` + `Media/` folder. See §18 for the full specification. |
| Printed wall | PDF (system) | Generated via the OS print dialog — `⌘P` (🍎) or Print… (📐). A4 portrait, 2 columns × 3 rows per page. See §11. |

Scene Cards does not export a scene list, schedule, or metadata to CSV,
JSON, or XML. All structured data lives inside the `.scenecards` package.

---

## A.3 Quick Reference

| You want to import… | Accepted formats |
|---|---|
| A script | PDF, FDX |
| A one-liner strip board | PDF |
| Sound reports | Sound Devices PDF, Sound Devices CSV, Zaxcom Nomad PDF |
| Camera / continuity / call sheets | PDF (attach-only) |
| A still for a card | JPEG, PNG, HEIC, TIFF, and others (see §A.1) |
| Any other production file | Drag to the reference carousel — any format accepted |
