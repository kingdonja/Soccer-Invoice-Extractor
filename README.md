# Nike Invoice Processing Hub

A browser-only tool that reads Nike invoice PDFs and pulls out the fields your
team reconciles, then exports them to Excel. No installation, no server, no Python.

## What it extracts

For each invoice: **PO Number, Invoice Number, Net Amount, Freight Amount,
Tax Amount, Total Due USD.**

## How to use it

1. Double-click **`index.html`** to open it in your web browser.
2. Drag one or many Nike invoice PDFs onto the box (or click to choose files).
3. Click **Process Invoices**. The results appear in a table.
4. Click **Download Excel** to save an `.xlsx` file for reconciliation.

## Good to know

- You need to be online the first time, so it can load two free tools it relies on:
  **PDF.js** (reads the PDFs) and **SheetJS** (builds the Excel file).
- Everything runs on your own computer — no invoice is ever uploaded anywhere.
- It has been tested against real Nike invoices, including long multi-page ones.

## How it handles the tricky parts

- The totals (Net/Freight/Tax/Total Due) aren't always on page 1 — on long
  invoices they're on a later page. The tool scans every page to find them and
  ignores the per-page "Page Subtotal" lines.
- The PO Number sits in a column that the PDF splits awkwardly. The tool rebuilds
  it from the page layout instead of the raw text, so it doesn't grab a neighboring
  number by mistake.
- Dollar amounts with commas (e.g. 1,363.50) are read correctly.
- Rows it can't fully read are shown in red rather than exported, so nothing wrong
  slips into your spreadsheet.

## Scope of this first version (v1)

Bulk upload, extraction of the six fields, on-screen table, and Excel export.

## Ideas for later

- CSV export.
- Duplicate invoice detection (same invoice dropped in twice).
- Grouping and subtotals by PO Number, plus a grand total.
- Support for additional vendors beyond Nike.
