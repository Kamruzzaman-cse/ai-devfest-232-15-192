# Tender Package Builder

A frontend-only web app that helps office staff turn a set of tender PDFs into one complete, checked and correctly ordered PDF package, ready to submit. Works fully in Bangla and English.

- **Name:** Kamruzzaman Amit
- **Registration number:** 232-15-192
- **Live link:** https://kamruzzaman-cse.github.io/ai-devfest-232-15-192/
- **Contest:** AI DevFest 2026 — AI Vibe-Coding Contest (Solo)

## How to run

Open the live link in the latest Google Chrome. No login and no install needed.

To run locally: download the repository and open `index.html` in Chrome (internet is needed once to load the `pdf-lib` library from CDN).

How to use:
1. Click **Open requirements.json** and choose the tender's `requirements.json`.
2. Add all PDF files (click the box or drag and drop).
3. Choose the right file for each document (or click **Auto-match by file name**), and enter expiry dates where asked.
4. When every status is OK or Not provided, click **Generate package**. The file downloads as `<tender_id>_Package.pdf`.

## Main features

- Loads `requirements.json`, shows tender details and the document list sorted by `order`
- Uploads many PDFs at once, shows file name and page count, user can remove any file
- Rejects non-PDF files with a clear message (checked by file content, not only the name)
- Matches files to documents: one file per document, one document per file, change or undo any time
- Expiry date entry for documents with `has_expiry = true`
- Live status for every document: Missing, Expiry date needed, Expired, Not provided, OK (expiring on the deadline day is still OK)
- Duplicate detection by SHA-256 content hash (even with different names); duplicates are marked and can't be used for different documents
- Generate button stays disabled while any blocking status exists, with a list of reasons
- Generated PDF: English cover page (tender ID, title, procuring entity, bidder, deadline, creation date, ordered document list), then all pages of each document in `order`, optional documents without a file skipped
- Footer `<tender_id> | Page X of Y` on every page including the cover. A blank strip is added below each document page, so the footer never covers the original content (rotated pages are handled)
- Download as `<tender_id>_Package.pdf`
- Full Bangla / English switch (all labels, buttons, messages; document names from `title_bn` / `title_en`)
- Responsive layout for desktop and mobile; all files stay in the browser

## Bonus features

- Index page after the cover, showing the start page of each document
- Export checklist as CSV (opens in Excel, Bangla text supported)
- Save and reopen work automatically using browser storage (IndexedDB)
- Auto-match suggestions from file names (prefers the newest year when several copies exist)
- Damaged or password-protected PDFs show a clear message instead of crashing

## Known problems

- The PDF cover and index are in English only (Bangla text on the PDF is not supported).
- Seal/signature placement and AI help bonus tasks are not done.
- Saved work is kept only in the same browser on the same computer.
- Expiry dates must be entered by the user; the app does not read dates from the PDF.

## AI tools used

- Claude (Anthropic) — planning, writing the code, testing and fixes

## Most useful prompt

> Build a frontend-only Tender Document Package Builder per the problem statement: load requirements.json sorted by order, upload multiple PDFs with page count, reject non-PDF, match files to documents (1:1), expiry date entry, status rules (Missing/Expiry date needed/Expired/Not provided/OK), SHA-256 duplicate detection, generate one PDF with English cover, documents in order and footer '<tender_id> | Page X of Y' that never covers content, download as <tender_id>_Package.pdf, full Bangla/English switch.

## Repository contents

- `index.html`, `style.css`, `i18n.js`, `pdfbuilder.js`, `app.js` — the app
- `output/T-2026-0417_Package.pdf` — package generated from the sample pack
- `screenshots/` — document status screenshot

## License

MIT
