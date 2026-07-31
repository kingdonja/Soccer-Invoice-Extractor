# Project notes for Claude Code

This file gives Claude Code context about the project so it can help effectively.

## What this project is

"Invoice Processing Hub" — a beginner-friendly, **browser-only web app** (HTML + CSS +
JavaScript in a single `index.html`) that extracts reconciliation fields from invoice
PDFs and exports them to Excel. It runs entirely in the browser — no backend, no
server, no Python.

Branding note: the visible UI is vendor-neutral (no "Nike" in the title or labels,
by request). The parsing itself currently targets the Nike Retail Services invoice
layout — keep the technical Nike references below, they are load-bearing.

The owner is a novice, not a professional programmer. When helping:

- Explain changes in plain language, avoiding jargon where possible.
- Keep everything in the single `index.html` file unless there's a strong reason not to.
- Keep the code readable and well-commented.
- Prefer small, understandable steps.

## Fields extracted

PO Number, Invoice Number, Gross Amount, Total Disc, Net Amount, Freight Amount,
Tax Amount, Total Due USD.

- Total Disc prints with a trailing minus on the invoice ("44.10-"); we record it
  as a positive number. Sanity check: Gross − Total Disc = Net on every invoice.

- **PO Number** is Nike's "Cust Prod PO #" column (e.g. `SOXRFL 06182026`), NOT
  Nike's internal "Order #". Its value wraps across two visual lines in the PDF.
- The money fields come from the invoice-level summary row labelled
  "Gross Amount / Total Disc / Net Amount / Freight Amount / Tax Amount / Total Due USD".

## How it works

- **PDF.js** (loaded from a CDN) reads the text out of each PDF.
- Text items are regrouped into visual lines by their y-position, which is more
  reliable than the raw text stream (needed because the PO Number wraps).
- The totals row is found by scanning every page for its label, so multi-page
  invoices work; "Page Subtotal" lines are ignored.
- **SheetJS** (loaded from a CDN) builds the `.xlsx` file in the browser.

## Testing note

Extraction was validated against 8 real Nike invoices (short and multi-page). If you
change the parsing, re-test against real sample invoices before trusting the output.

Known format quirks (learned from real invoices — don't "simplify" these away):

- Amounts in the totals row are NOT always two-decimal: Nike prints "13.9" for
  $13.90 and a bare "0" for $0.00. The number matcher must accept whole numbers
  and one-decimal numbers, not just xx.xx.
- Freight can legitimately be $0.00.
- The totals row can appear on page 1, 2, or 3 depending on invoice length.

## Duplicate detection & totals (implemented)

- Duplicates are detected by invoice number (not file name). First copy counts;
  repeats are flagged amber and excluded from totals and the Excel export.
- The table has a tfoot Totals row; the Excel export ends with a TOTALS row.
  Both sum only non-error, non-duplicate rows. Keep those two exclusions in sync.

## Ideas for later

- CSV export; grouping/subtotals by PO Number; more vendors.
