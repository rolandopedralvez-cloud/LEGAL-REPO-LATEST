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
│   ├── html/                     ← 51 converted documents (the actual legal corpus)
│   └── source/                   ← notes on skipped/OCR-flagged source PDFs
├── incoming-raw/                 ← manually-downloaded source PDFs awaiting conversion
└── ui/
    ├── index.html                ← the dashboard app (Tabler-based, no build step)
    └── data/
        └── documents.js          ← document data the dashboard reads
```

## Current status: 213 documents converted (target raised — see below)

**Converted so far:** 23 foundational laws (Republic Acts, foundational Commonwealth Act/Presidential
Decrees, and Executive Orders), 3 Department Orders, 11 Memorandum Orders, and 174 Memorandum
Circulars/Joint Circulars spanning categories including General, Amateur, Broadcast, Telecom, Maritime
(SOLAS/GMDSS/STCW/GMDSS/NAVTEX/EPIRB), Fixed/Land Mobile, CPE, Value Added Services/VoIP, Radio
Training Center, Civic Group, Low Power Equipment, Cellular Mobile, Wireless Data Network, Radio
Operator's Certificate, Radio Communication Dealers, Cable Television, Market Competition/New
Major Player, Satellite Communications (domestic and international, plus TVRO and ESVs), Repeater
Networks, Short-Range Radio/Devices, RFID, Restricted Land Mobile, Personal Radio Service,
Government Personal Radio Service, Trunked Radio (PTRS), Content Classification (MTRCB/VRB), and
Spectrum/Fee Administration. Round 8 added 20 more documents, including four 1972 martial-law-era
circulars issued by the Radio Control Office (NTC's predecessor agency) — one directly invoking
Proclamation No. 1081 — a paired set on the 430-440 MHz amateur/commercial spectrum dispute, a
paired set of sequential VHF-equipment deadline extensions for fishing vessels, and a pair of
program-standards content-restriction circulars (1985 and its 2001 reiteration amid a reported
destabilization concern). Round 9 added 20 more documents, including Executive Order No. 205
(1987 CATV regulation) and a range of broadcast, maritime, and CATV circulars from the 1980s-2000s.
Round 10 added 16 more documents, including foundational laws Commonwealth Act 146 (the 1936
Public Service Act), Presidential Decrees 1986 and 1987 (creating the MTRCB and VRB content
classification boards), Presidential Decree 576-A, and Act No. 3396, plus spectrum-allocation and
GMDSS/RTC-related circulars. Round 11 added 20 more documents, including a detailed revised CPE
interface standards circular and a broad set of 1980s-2000s amendment circulars covering amateur
radio, radio operator certification, maritime safety equipment, and spectrum administration.
Round 12 added 5 more documents recovered via a higher-resolution re-OCR pass (250dpi + Tesseract)
on source PDFs whose baked-in text layer was too garbled for direct `pdftotext` extraction: two
spectrum-allocation circulars (BWA at 3300-3400 MHz, and the 5351.5-5366.5 kHz amateur radio band),
an amendment updating short-range-device technical parameters, an Ultra-Wide Band (UWB) device
definition and operating-conditions amendment, and a maritime radio-station-license deletion
certificate guideline. Round 13 added 6 more documents, all recovered via the same 250dpi re-OCR
technique: a joint NTC-DICT-DTI circular on one-year prepaid load expiration, a TV White Space
spectrum-access circular, a reduced SMS/voice interconnection charge circular, additional CATV
application evaluation guidelines, the detailed Implementing Rules and Regulations for Digital
Terrestrial Television (DTTB) channel assignment in Mega Manila, and an updated ship radio
equipment/operator-certification circular for domestic-route vessels. Round 14 added 7 more
documents, the last round of this session's "keep going 5 times" run (batches 10-14), all
recovered via the same re-OCR technique: an updated short-range-device frequency table, an
extended compliance timeline for ISDB-T Emergency Warning Broadcast System receivers, electronic
billing (e-billing) consumer guidelines, the PTE-identifier assignment scheme for Metro Manila's
8-digit exchange-code migration, temporary permit guidelines for newly acquired ship stations,
fixed broadband quality-of-service measurement rules, and ISP content-filtering guidelines under
the Anti-Child Pornography Act (recovered from a fax-quality scan, with residual uncertain details
marked rather than guessed).

All 213 pass `scripts/validate.py` with 0 errors.

**Target raised:** the user manually downloaded the full NTC Region VII laws/regulations archive
(~300 PDFs) into `incoming-raw/`. After dedup and matching against already-converted documents,
roughly 98 distinct documents remain to be converted — far beyond the original 50-document
target. Rounds 12-14 added 18 documents recovered by re-OCR rather than direct extraction (see
below); all still include verbatim full text. The rest are being converted in successive batches.
See `incoming-raw/` for what's still pending.

**Known gaps (scanned/non-machine-readable sources, not converted):** MC 03-03-2005A
(`examples/source/mc-03-03-2005a-needs-ocr.txt`), RA 8439
(`examples/source/ra-8439-needs-ocr.txt`). Some `incoming-raw/` PDFs required OCR (garbled or
empty text layers) — those have been re-extracted via OCR and are queued for the next conversion
batch rather than being skipped outright.

**Out of scope, found in incoming-raw:** `EO_298.pdf` turned out to be about government
travel-allowance rates, unrelated to NTC/telecommunications — it will not be converted into this
repository.

**Verbatim full text:** the dashboard's "Full Original Text" toggle now has real verbatim text for
184 of 213 documents — the original 3, 23 backfilled in round 3, 10 in round 4, 15 in round 5, 20
in round 6, 19 in round 7, 20 in round 8, 20 in round 9, 16 in round 10, 20 in round 11, 5 in round
12, 6 in round 13, and all 7 newly converted in round 14. Text was extracted directly from each
source PDF via `pdftotext`, with OCR (`tesseract`, at 250dpi where the default extraction was too
garbled) as
fallback where the
PDF's text layer was garbled or missing — never paraphrased or reconstructed from the summary. A
few signatory names in the round-12 documents remain partially illegible even after re-OCR and are
marked as such in the verbatim text rather than guessed at. The remaining Memorandum Circulars
still show a clear notice and fall back to the summary view rather than presenting a paraphrase as
the original; full-text backfill for those continues in future batches.

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
