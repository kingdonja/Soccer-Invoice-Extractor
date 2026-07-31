# Invoice Processing Hub

A browser-only tool that reads invoice PDFs and pulls out the fields your
team reconciles, then exports them to Excel. No installation, no server, no Python.

## What it extracts

For each invoice: **PO Number, Invoice Number, Gross Amount, Total Disc,
Net Amount, Freight Amount, Tax Amount, Total Due USD.**

(Total Disc is shown as a positive number — it's the discount that was
subtracted: Gross − Total Disc = Net.)

## How to use it

1. Double-click **`index.html`** to open it in your web browser.
2. Drag one or many invoice PDFs onto the box (or click to choose files).
3. Click **Process Invoices**. The results appear in a table.
4. Click **Download Excel** to save an `.xlsx` file for reconciliation.

## Good to know

- You need to be online the first time, so it can load two free tools it relies on:
  **PDF.js** (reads the PDFs) and **SheetJS** (builds the Excel file).
- Everything runs on your own computer — no invoice is ever uploaded anywhere.
- Extraction is currently tuned to the Nike Retail Services invoice layout and has
  been tested against real invoices, including long multi-page ones. Other vendors'
  invoice formats can be added later.

## How it handles the tricky parts

- The totals (Net/Freight/Tax/Total Due) aren't always on page 1 — on long
  invoices they're on a later page. The tool scans every page to find them and
  ignores the per-page "Page Subtotal" lines.
- The PO Number sits in a column that the PDF splits awkwardly. The tool rebuilds
  it from the page layout instead of the raw text, so it doesn't grab a neighboring
  number by mistake.
- Dollar amounts with commas (e.g. 1,363.50), one-decimal amounts (13.9), and
  zero amounts (a freight of 0) are all read correctly.
- Rows it can't fully read are shown in red rather than exported, so nothing wrong
  slips into your spreadsheet.

## Duplicate detection

If the same invoice number is dropped in more than once (even under a different
file name), the first copy counts and every repeat is highlighted in amber,
labeled as a duplicate, and left out of the totals and the Excel export — so
nothing gets double-counted.

## Totals

A bold Totals row at the bottom of the table (and a TOTALS row in the Excel
export) sums every column across the successfully-read, non-duplicate invoices.

## Ideas for later

- CSV export.
- Grouping and subtotals by PO Number.
- Support for additional vendors.
