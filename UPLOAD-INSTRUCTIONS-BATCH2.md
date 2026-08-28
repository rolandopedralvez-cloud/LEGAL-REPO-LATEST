# Upload instructions — batch bringing LEGAL-REPO-LATEST to 51 documents

This one zip covers TWO pending rounds at once (the original 4-doc batch you hadn't uploaded yet,
plus this session's 15-document batch from your `incoming-raw/` files) — so you only need to do
this once instead of twice.

## 1. New files — add to `examples/html/`

Upload these 19 files into your repo's `examples/html/` folder (all brand new, no conflicts):

eo-59.html, pd-576-a.html, ca-146.html, do-5.html, act-3396.html, eo-109.html, eo-196.html,
eo-205.html, eo-255.html, eo-436.html, eo-454.html, eo-467.html, eo-468.html, eo-47.html,
eo-648.html, pd-1986.html, pd-1987.html, do-7.html, do-11.html

## 2. New file — add to `examples/source/`

- `ra-8439-needs-ocr.txt`

## 3. Replace existing file — `examples/html/mc-10-07-2007.html`

Open the existing file on GitHub, replace its full content with the version in this zip. The only
change: its existing plain-text mentions of "EO 59" and "Commonwealth Act 146" are now hyperlinked
to the new documents, and both were added to its `cross_references` metadata.

## 4. Replace existing file — `ui/data/documents.js`

Replace with the attached version. It now has 51 entries (was 32) — 19 new entries appended,
nothing else reordered or changed.

## 5. Replace existing file — `README.md`

Replace with the attached version. Covers the new document count (51), the raised target (your
~300-PDF `incoming-raw/` upload changed the scope — see the README's "Current status" section for
the full explanation), known gaps, and one document (`EO_298.pdf`) identified as out of scope
(it's about government travel allowances, not telecommunications) and excluded from conversion.

## What's still pending (not in this batch)

Your `incoming-raw/` folder has roughly 275 more distinct documents after dedup. Some needed OCR
because their PDFs had garbled or empty text layers — RA_10844_DICT, RA_9775 (Anti-Child
Pornography Act), RA_8370, and RA_9485 have already been OCR'd successfully and are queued for the
next batch, along with the rest of the Memorandum Circulars, Memorandum Orders, and Office Orders
in that folder. I'll continue converting these in further batches of similar size.

## Verification performed before this delivery

- All 19 new documents' text was read directly from their source PDFs (via `pdftotext`, with OCR
  fallback for garbled/scanned ones) — no content was written from assumption or paraphrase alone.
- `scripts/validate.py` against all 51 files: **0 errors**.
- `node --check` on `documents.js`: valid syntax.
- Document-ID cross-check: all 51 `examples/html/*.html` filenames exactly match the 51 `id`
  fields in `documents.js` — no duplicates, no drift.
