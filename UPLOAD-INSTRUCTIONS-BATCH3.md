# Upload instructions — batch bringing LEGAL-REPO-LATEST to 55 documents + full text backfill

## 1. New files — add to `examples/html/`

- `ra-10844.html` (DICT Act of 2015)
- `ra-9775.html` (Anti-Child Pornography Act of 2009)
- `ra-8370.html` (Children's Television Act of 1997)
- `ra-9485.html` (Anti-Red Tape Act of 2007)

## 2. Replace existing file — `ui/data/documents.js`

Replace with the attached version (now ~437KB, up from a much smaller file — this is expected,
since it now carries verbatim full text for 26 documents). It has 55 entries total (was 51) — 4
new entries appended, plus a `fullText` field added to 23 previously summary-only entries:
act-3396, eo-109, eo-196, eo-205, eo-255, eo-436, eo-454, eo-467, eo-468, eo-47, eo-648, pd-1986,
pd-1987, do-7, do-11, eo-59, pd-576-a, do-5, ca-146 (19 from the last batch), plus the 4 new RAs.

## 3. Replace existing file — `README.md`

Reflects the new document count (55), the full-text backfill progress (26 of 55), and the
methodology note on how full text was extracted and verified.

## How the full text was sourced

For every document that now has `fullText`, the text came directly from the source PDF already in
your `incoming-raw/` folder (or the repo root, for CA 146), via `pdftotext`. Four PDFs
(RA 10844, RA 9775, RA 8370, RA 9485) had scanned/garbled text layers, so those were OCR'd with
`tesseract` at high resolution instead — checked for readability before being used. Two more
(EO 47, EO 648) had a baked-in bad OCR layer from whoever originally scanned them, so I re-OCR'd
those at higher resolution too rather than using the garbled text. Nothing was paraphrased or
reconstructed — if a document doesn't have `fullText` yet, it's because it hasn't been through
this process yet, not because the text was unusable.

## Verification performed before this delivery

- `scripts/validate.py` against all 55 files: **0 errors**.
- `node --check` on `documents.js`: valid syntax.
- Document-ID cross-check: all 55 `examples/html/*.html` filenames exactly match the 55 `id`
  fields in `documents.js` — no duplicates, no drift.
- Manually confirmed every one of the 26 `fullText` fields is present and non-empty by loading
  `documents.js` in Node and checking character counts.

## What's still pending

~256 more documents remain in `incoming-raw/` (and the ~44 still-loose PDFs at the repo root) to
convert — mostly Memorandum Circulars and Memorandum Orders. Full-text backfill for the 29
existing Memorandum Circulars (beyond the 3 already done) is also still outstanding.
