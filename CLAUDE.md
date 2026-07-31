# Project notes for Claude Code

This file gives Claude Code context about the project so it can help effectively.

## What this project is

A beginner-friendly, **browser-only web app** (HTML + CSS + JavaScript in a single
`index.html`) that extracts reconciliation fields from Nike invoice PDFs and exports
them to Excel. It runs entirely in the browser — no backend, no server, no Python.

The owner is a novice, not a professional programmer. When helping:

- Explain changes in plain language, avoiding jargon where possible.
- Keep everything in the single `index.html` file unless there's a strong reason not to.
- Keep the code readable and well-commented.
- Prefer small, understandable steps.

## Fields extracted

PO Number, Invoice Number, Net Amount, Freight Amount, Tax Amount, Total Due USD.

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

Extraction was validated against 5 real Nike invoices (short and multi-page). If you
change the parsing, re-test against real sample invoices before trusting the output.

## Ideas for later

- CSV export; duplicate detection; grouping/subtotals by PO Number; more vendors.
