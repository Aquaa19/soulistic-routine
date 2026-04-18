# Soulistic Routine Maker

An elegant static web app for building, previewing, and printing weekly class routines for **Soulistic IND**.

[Live Demo](https://aquaa19.github.io/soulistic-routine/) | [Admin Panel](./index.html) | [Printable Template](./routine.html)

## Overview

This project is a lightweight routine generator built with plain HTML, CSS, and JavaScript. It provides an admin-facing editor in `index.html` and a styled printable routine view in `routine.html`.

The editor sends schedule data to the preview using `window.postMessage()`, allowing the final routine to update instantly inside an embedded iframe.

## Highlights

- Weekly schedule support for Monday through Sunday
- Configurable time slots from `2:00 PM` to `8:00 PM`
- Subject selection with teacher initials
- Hideable time-slot columns for cleaner final output
- Live preview inside the admin interface
- Print-friendly branded layout for final routine output
- No framework, no backend, no build step

## Project Structure

| File | Purpose |
| --- | --- |
| [index.html](./index.html) | Admin interface for entering class, session, subject assignments, initials, and visible slots |
| [routine.html](./routine.html) | Styled preview and printable routine layout |
| [soul-logo.jpg](./soul-logo.jpg) | Logo used in the preview header |
| [README.md](./README.md) | Project documentation |

## How It Works

### Admin Panel

`index.html` generates the routine editor dynamically using:

- `days` for weekly rows
- `slots` for time-based columns
- `subjectList` for predefined subject and teacher mappings

Each editable cell contains:

- a subject dropdown
- an initials input

### Live Preview

When the user clicks `Push to Routine Preview`, the admin page gathers:

- class name
- academic session
- active time slots
- day-wise subject assignments

It then sends the data to the embedded preview:

```js
iframe.contentWindow.postMessage(data, '*');
```

`routine.html` listens for the message and re-renders the badges, headers, and full routine table in place.

### Printable Routine

The printable page includes:

- branded header and footer
- subject-specific color styling
- compact tabular layout
- print-ready formatting through `window.print()`

## Configured Subjects

The current routine editor includes these built-in subject options:

- Hindi
- Physics
- Biology
- Science
- History
- Geography
- SST
- Mathematics
- Bengali
- Chemistry
- English
- Computer
- Booster Dose

Teacher initials are auto-filled for many of these entries from the `subjectList` configuration in `index.html`.

## Running Locally

No installation is required.

### Open Directly

Open `index.html` in your browser. For most local use cases, that is enough.

### Run a Local Server

If your browser applies stricter file restrictions, serve the folder locally:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/index.html
```

## Recommended Workflow

1. Open `index.html`.
2. Enter the class name.
3. Choose the academic session.
4. Select subjects for each day and slot.
5. Adjust teacher initials where needed.
6. Hide unused columns.
7. Click `Push to Routine Preview`.
8. Review the formatted output.
9. Print the routine from the preview page.

## Technical Notes

- Built entirely with vanilla HTML, CSS, and JavaScript
- Uses an iframe-based preview flow
- Loads Google Fonts in `routine.html`
- Styles subject cards through the `subjectStyles` object
- Resets the editor back to a default session and blank schedule

## Current Limitations

- No persistence; refresh clears the entered routine
- No backend or user authentication
- Subject list is hardcoded
- `postMessage(..., '*')` is broad and can be restricted further for deployed environments

## Good Next Improvements

- Save and restore routines with `localStorage`
- Export and import routine data as JSON
- Make subjects and teacher mappings editable from the UI
- Add validation before printing
- Tighten `postMessage` target origin handling
