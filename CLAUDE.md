# Project notes for Claude Code

This file gives Claude Code context about the project so it can help effectively.

## What this project is

A simple, beginner-friendly **web app** that reads a PDF (such as a soccer camp
invoice) and produces a formatted report. It runs entirely in the browser.

The owner is a novice, not a professional programmer. When helping:

- Explain changes in plain language, avoiding jargon where possible.
- Keep everything in the single `index.html` file unless there's a strong reason not to.
- Keep the code simple and well-commented.
- Prefer small, understandable steps over clever or advanced solutions.

## How it works

- `index.html` is the whole app: HTML (structure) + CSS (styling) + JavaScript (logic).
- It uses **PDF.js** (loaded from the cdnjs CDN) to read PDF files in the browser.
- Drag-and-drop and a click-to-choose file picker both feed the same `handleFile` routine.
- The report is shown on the page and can be downloaded as a `.txt` file.

## Conventions

- No build step, no server, no install — the user just opens `index.html`.
- Keep external dependencies to a minimum; right now the only one is PDF.js.

## Ideas for later

- Extract specific invoice fields (total, date, player/team, invoice number).
- Support multiple PDFs at once.
- Offer PDF or spreadsheet output.
