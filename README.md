# Mileage Chart Project

A Google Apps Script project bound to a Google Sheet that calculates mileage between particular campuses and facilities. It includes a `numberOfMiles(start, destination)` custom function for use in Google Sheets and a `ClearForm` macro to reset the entry form.

## User Impact
This project is meant to save users time from having to have a separate mileage calculation excel sheet open and inputting data on that sheet for each line in the mileage reimbursement form. This cuts down on the time it takes the user to complete the reimbursement form.

## Prerequisites

- [Node.js](https://nodejs.org/) (for `clasp`)
- [clasp](https://github.com/google/clasp) — the Google Apps Script CLI

```bash
npm install -g @google/clasp
```

- A Google account with [Apps Script API enabled](https://script.google.com/home/usersettings)

## Setup

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd mileage-2026
```

### 2. Set up the Google Sheet

The template sheet is included in this repo as `mileage-template-2026.xlsx`. It contains all the formulas, dropdowns, styles, and merged cells needed for the form to work.

1. Go to [Google Drive](https://drive.google.com)
2. Click **New → File upload** and select `mileage-template-2026.xlsx`
3. Once uploaded, right-click the file and choose **Open with → Google Sheets** — Google will convert it automatically
4. Keep this sheet open; you'll link the Apps Script project to it in the next steps

### 3. Log in to clasp

```bash
clasp login
```

### 4. Link the Apps Script project to your sheet

Open the Google Sheet from Step 2, then go to **Extensions → Apps Script**. This opens a script project already bound to that sheet. Copy the script ID from **Project Settings**, then update `.clasp.json`:

```json
{
  "scriptId": "YOUR_SCRIPT_ID_HERE",
  "rootDir": "."
}
```

### 5. Push the code

```bash
clasp push
```

## Usage

### `numberOfMiles(start, destination)`

A custom Google Sheets function that returns the mileage between two NISD locations.

```
=numberOfMiles("Adams Hill E.S.", "Clark H.S.")
```

Both arguments must match a location name exactly as listed in the mileage chart inside `code.js`.

### `ClearForm` macro

Clears the input range `C16:M29` on the active sheet. It is bound to the keyboard shortcut **Ctrl+Alt+Shift+1** and also available under **Extensions > Macros > ClearForm**.

## Project Structure

| File | Description |
|------|-------------|
| `code.js` | Main script — mileage lookup function and ClearForm macro |
| `appsscript.json` | Apps Script manifest — runtime settings and macro bindings |
| `.clasp.json` | clasp config — links this directory to an Apps Script project |
| `mileage-template-2026.xlsx` | Sheet template — upload to Google Drive and convert to Google Sheets |
| `mlgcht2026unlocked.csv` | Source mileage data |

## Credits & Origin
This project was originally conceived and developed by Alvaro Gomez during his tenure at Northside ISD. This public version has been sanitized and refactored. Campus distances will need to be updated in the `code.js` file before general use.