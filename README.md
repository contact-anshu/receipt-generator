# Rapido Receipt Generator

> **A browser-based receipt mockup generator for demos and UI testing.**  
> Ride IDs, driver names, vehicle numbers, and ride times are generated data. This tool is not affiliated with Rapido, does not verify real trips, and does **not** create official receipts or documents suitable for expense claims or reimbursement.

Turn rows from an Excel claims sheet into a live, branded-style receipt preview. Select rides, inspect the generated details, and export a preview as PNG or PDF — all from a single HTML page.

## What it does

- Reads ride dates, drop locations, and claimed amounts from the **first worksheet** of an `.xlsx` or `.xls` file.
- Builds an interactive table so you can select a ride and preview its receipt.
- Lets you set the displayed customer name, pickup location, vehicle state, and vehicle mode.
- Exports the active preview as a PNG image or PDF, or triggers a separate PDF download for each loaded row.
- Runs in the browser without an app server, database, or build step.

## Quick start

1. Download or clone this project.
2. Open `index.html` in a modern browser with an internet connection.
3. Set the customer, pickup location, vehicle state, and vehicle mode.
4. Upload an Excel workbook containing the expected columns.
5. Select **Generate Previews**, choose a ride in the table, and export the preview.

The included `logo.png` is used in the receipt preview. Keep it beside `index.html`.

## Excel input

The app reads the first worksheet and recognizes these column names:

| Required value | Accepted column names |
|---|---|
| Date | `DATE`, `Date`, `date` |
| Drop location | `Location To`, `Location to`, `DROP`, `Drop` |
| Claimed amount | `Claimed Amount`, `CLAIMED AMOUNT`, `Amount`, `Price` |

Each row needs a date, a drop location, and a numeric amount. Rows that do not meet those checks, or whose date cannot be parsed, are skipped. Excel serial dates and date strings are supported.

## How the generated data works

Only the date, drop location, and amount come from the workbook. The app **does not** look up or verify real rides. For each accepted row, it creates:

- A random ride ID
- A random driver name
- A random vehicle number using the selected state prefix
- A random time between 10:00 AM and 2:59 PM on the row's date

These values are placeholders. The generated preview should be treated as sample content, not evidence of a trip or payment. Choose the vehicle state before uploading; it is used when vehicle numbers are generated.

## Exports

- **PNG:** captures the active receipt preview at 2× scale.
- **PDF:** places the same captured preview into a single-page PDF.
- **Download All PDFs:** starts an individual PDF download for every loaded ride; it does not create a combined PDF or ZIP archive. Your browser may prompt you to allow multiple downloads.

## Tech stack

- Semantic HTML and vanilla JavaScript
- Tailwind CSS via CDN for layout and styling
- SheetJS (`xlsx`) for workbook parsing
- `html2canvas` for receipt image capture
- `jsPDF` for PDF generation

There is no backend or build pipeline. The page loads its libraries and Inter font from third-party CDNs, so an internet connection is required. Workbook parsing and receipt generation happen in the browser; the app contains no code that sends workbook contents to an application server.

## Project layout

```text
.
├── index.html   # UI, styling, Excel parsing, preview, and export logic
├── logo.png     # Image displayed on the receipt preview
└── README.md
```

## Important limitations

- This is a mockup/demo utility, not an official Rapido product or receipt generator.
- Generated ride IDs, driver details, vehicle numbers, and times are random and may not correspond to real-world records.
- It does not validate claims, calculate fares, or confirm that a ride occurred.
- Do not use its output for reimbursement, accounting, tax, insurance, or other official purposes.
- The application has no automated tests or package manager setup; it is a standalone HTML file.
