# Soccer Invoice Extractor

A simple web app that reads a PDF (such as an invoice) and produces a clean,
readable report — all inside your web browser. Nothing to install.

## How to use it

1. Double-click **`index.html`**. It opens in your web browser.
2. Drag a PDF onto the box (or click the box to choose a file).
3. A report appears on the page: the file name, number of pages, total word
   count, and the text from each page.
4. Click **Download report** to save it as a text file.

## What it's built with

- **HTML** — the structure of the page
- **CSS** — how the page looks
- **JavaScript** — the part that reads the PDF and builds the report

All three live in the single `index.html` file. To read PDFs it uses
**PDF.js**, a free tool made by Mozilla, loaded automatically from the internet.

## Good to know

- You need to be online the first time you use it (so it can load PDF.js).
- Everything happens on your own computer — your PDF is never uploaded anywhere.
- Scanned PDFs that are really just images (no real text inside) won't have text
  to extract; the report will say so for those pages.

## Ideas for later

- Pull out specific invoice fields (total, date, player/team name, invoice number).
- Handle several PDFs at once.
- Save the report as a nicely formatted PDF or spreadsheet instead of plain text.
