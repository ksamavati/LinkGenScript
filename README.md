# LinkGenScript

A web-based tool that automatically generates hyperlinked articles by intelligently linking keyword phrases found in article titles. The application fetches article metadata and a keyword list from Google Sheets, then renders a formatted HTML bulleted list with contextual hyperlinks embedded in each title.

## Features

- Authenticates with Google via OAuth 2.0 (read-only spreadsheet access)
- Fetches article titles, URLs, and a keyword phrase list from Google Sheets
- Intelligently selects a keyword to hyperlink in each title using a priority-based fallback algorithm:
  1. First matching keyword phrase from the keyword sheet
  2. First word ending in `s`
  3. First word ending in `ing`
  4. Third word (or last word if the title has fewer than four words)
- Renders results as a clean HTML bulleted list

## Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | HTML5, JavaScript (ES5) |
| APIs | Google Sheets API v4, Google Sign-In |
| Build Tools | Grunt, Gulp (configured, not actively used) |
| IDE | NetBeans |

## Getting Started

### Prerequisites

- A web server (or open the file locally in a browser)
- A [Google Cloud project](https://console.developers.google.com/) with the **Google Sheets API** enabled
- A Google OAuth 2.0 **Client ID** (Web application type)

### Google Sheets Setup

The application expects two Google Sheets:

| Sheet | Purpose | Range |
|-------|---------|-------|
| **Funding sheet** | Article titles (column A) and URLs (column B) | `Funding!A2:B` |
| **Keywords sheet** | Keyword phrases, one per row (column A) | `keyphrases!A1:A` |

### Configuration

Open `public_html/index.html` and update the following constants near the top of the `<script>` block:

```js
// Replace with your Google OAuth 2.0 Client ID
var CLIENT_ID = 'YOUR_CLIENT_ID.apps.googleusercontent.com';

// Replace with the ID of your Funding spreadsheet
// (the long string in the sheet's URL)
var fundingSheetId = 'YOUR_FUNDING_SHEET_ID';

// Replace with the ID of your Keywords spreadsheet
var keywordsSheetId = 'YOUR_KEYWORDS_SHEET_ID';
```

> **Note:** Keep your Client ID restricted to the specific origin(s) where the app will run in the Google Cloud Console to limit exposure.

### Running the App

1. Host `public_html/index.html` on a web server, or open it directly in a browser.
2. Click **Authorize** and complete the Google sign-in flow.
3. Click **Generate Links** to fetch data from your sheets and produce the linked HTML output.

## Project Structure

```
LinkGenScript/
├── public_html/
│   ├── index.html                              # Current version of the app
│   └── Version 1.2 (Pulls keywords from sheet)/
│       ├── index.html                          # Version 1.2 source
│       └── patch notes.txt                     # v1.2 release notes
├── nbproject/                                  # NetBeans IDE project files
├── package.json
├── bower.json
├── Gruntfile.js
├── gulpfile.js
└── README.md
```

## Versioning

| Version | Changes |
|---------|---------|
| 1.2 | Keywords are now pulled dynamically from a Google Sheet; two-word phrase linking supported |
| 1.0 | Initial release with hardcoded keyword list |

## License

This project does not currently specify a license.
