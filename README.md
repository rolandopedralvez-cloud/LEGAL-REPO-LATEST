# NTC Legal Repository

A structured, searchable repository of NTC Region VII (National Telecommunications Commission,
Central Visayas, Philippines) laws, Executive Orders, and Memorandum Circulars — converted from
their original PDFs into semantic HTML with structured metadata, plus a working dashboard UI to
browse, search, and manage them for case work.

Source site: https://region7.ntc.gov.ph/laws-rules-and-regulations/

## Repo structure

```
├── README.md                   ← this file
├── docs/
│   ├── design.md                ← full architecture & design doc
│   ├── conversion-workflow.md   ← how source PDFs become structured HTML
│   └── accessibility.md         ← WCAG checklist for public-facing use
├── schema/
│   └── document-schema.json     ← metadata contract every document follows
├── scripts/
│   └── validate.py               ← checks converted docs for missing IDs/metadata/broken links
├── examples/
│   ├── html/                     ← 32 converted documents (the actual legal corpus)
│   └── source/                   ← notes on skipped/OCR-flagged source PDFs
└── ui/
    ├── index.html                ← the dashboard app (Tabler-based, no build step)
    └── data/
        └── documents.js          ← document data the dashboard reads
```

## Current status: 32 of 50 target documents

**Converted so far:** 3 core laws (RA 7925, EO 546, Act 3846) + 29 Memorandum Circulars spanning
16 categories (General, Amateur, Broadcast, Telecom, Maritime, Fixed/Land Mobile, CPE, Value
Added, Radio Training Center, Civic Group, Low Power Equipment, Cellular Mobile, Wireless Data
Network, Radio Operator's Certificate, Radio Communication Dealers).

All 32 pass `scripts/validate.py` with 0 errors.

**Known gap:** one source PDF (MC 03-03-2005A) is a scanned image with no extractable text and is
flagged in `examples/source/mc-03-03-2005a-needs-ocr.txt` rather than converted with guessed content.

**Verbatim full text:** the dashboard's "Full Original Text" toggle currently has real verbatim
text backfilled for 3 of 32 documents (MC 04-89, MC 06-04-99, MC 10-07-2007). The rest show a
clear notice and fall back to the summary view rather than presenting a paraphrase as the original.

## Using the dashboard (ui/)

No build step — open `ui/index.html` directly in a browser, or serve the folder:

```bash
cd ui
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

**Features:**
- Search with inline term highlighting
- Sidebar mirrors region7.ntc.gov.ph's actual category structure (Republic Acts, Presidential
  Decrees, Department Orders, Executive Orders, plus lettered A–O Memorandum Circular
  sub-categories with document counts; empty categories shown greyed out, not hidden)
- Case Binder — pin documents to a working case file (persists via browser localStorage),
  printable as one combined packet
- Print / Save PDF — formatted print view with a formal citation line
- Summary vs. Full Original Text toggle per document

## Converting more documents

1. Fetch the real source PDF from region7.ntc.gov.ph (or another official government source if
   not hosted there). Never fabricate content — if the PDF has no extractable text, flag it in
   `examples/source/[name]-needs-ocr.txt` and skip conversion.
2. Convert into the same HTML structure as existing files in `examples/html/`, including the
   JSON metadata comment block at the top (see `schema/document-schema.json` for the contract).
3. Run `python3 scripts/validate.py examples/html/` — must show 0 errors before committing.
4. Add a matching entry to `ui/data/documents.js` so it appears in the dashboard.
5. Update this README's counts.
6. Before committing: recount files on disk and cross-check against what's listed here — they
   must match exactly. This step has caught real problems before; don't skip it.

## Verification discipline

This repository had multiple instances of unverified/fabricated content appearing during
development, which were caught and removed before being finalized. Every document currently in
`examples/html/` has been cross-checked against an actual source fetch. If extending this repo,
maintain the same discipline: verify before converting, recount before committing, cross-check
the README against the actual file list every time.
