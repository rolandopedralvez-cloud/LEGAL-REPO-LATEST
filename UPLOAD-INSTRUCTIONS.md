# Upload instructions — catch-up package (55 → 213 documents)

I checked your live GitHub repo (rolandopedralvez-cloud/LEGAL-REPO-LATEST) before building this.
It currently has **55 documents** (more than the 51 I'd last confirmed — looks like you uploaded
a bit more since). This package brings it up to the full **213 documents** built so far, in one
step.

## What's in this zip

- `examples/html/` — **158 new HTML files** (every document that's on my side but not yet on
  GitHub). None of your existing 55 files are touched or duplicated in this folder.
- `ui/data/documents.js` — the **full, replace-in-place** file with all 213 entries (your existing
  55 plus the 158 new ones). This is a superset, not a diff — just overwrite your current copy.
- `README.md` — the **full, replace-in-place** file with updated document counts and narrative.

## How to upload

1. Copy the 158 files from this zip's `examples/html/` into your repo's `examples/html/` folder
   (these are new files, nothing to overwrite there).
2. Replace your repo's `ui/data/documents.js` with the one in this zip.
3. Replace your repo's `README.md` with the one in this zip.
4. Commit and push.

That's it — no other files need to change.

## Verification performed before packaging this

- Fetched your live repo (`git fetch origin`) and diffed its 55 `examples/html/*.html` filenames
  against my local 213 — confirmed all 55 of your existing documents are also present on my side
  (no orphans, nothing on GitHub that would get lost), and identified exactly 158 documents that
  exist locally but not yet on GitHub.
- `scripts/validate.py` against all 213 local HTML files: **0 errors**.
- `node --check` on the full `documents.js`: valid syntax.
- Document-ID cross-check: all 213 `examples/html/*.html` filenames exactly match the 213 `id`
  fields in `documents.js` — no duplicates, no drift.

## Notes

- Two documents in the source archive have partially illegible printed circular numbers even after
  re-OCR (`mc-01-03-2017`'s own scan reads ambiguously as "01-03-2017" or "01-03-2019"; a handful
  of signatory names across a few 2016-2020 circulars are similarly uncertain). These are marked
  as such directly in each document's verbatim full text rather than guessed at.
- Of the 213 documents, 184 have verbatim full text extracted from the source PDFs; the remaining
  29 (mostly older Memorandum Circulars not yet backfilled) show a structured summary only, with a
  clear notice in place of a fabricated "original text."
- Roughly 98 more source documents remain unconverted in `incoming-raw/` for future batches.
