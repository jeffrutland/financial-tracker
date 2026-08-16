# Financial Tracker

A lightweight, browser-based financial data tracker that visualizes daily closing values across one or more time series. The app stores data locally in the browser and automatically fetches historical Dow Jones Industrial Average data via the [Financial Modeling Prep API](https://financialmodelingprep.com/developer/docs/).

## Features

- **Dow Jones Automatic Data** — On first load, the app fetches historical Dow Jones Industrial Average (`^DJI`) closing prices from the Financial Modeling Prep API and saves them locally for offline use.
- **Multiple Series** — In addition to the Dow Jones, you can create custom named series (e.g. "S&P 500", "Bitcoin", etc.). Each series displays its own line chart.
- **Live Charting** — Charts are rendered with [Chart.js](https://www.chartjs.org/) using [Luxon](https://moment.github.io/luxon/) for time-axis formatting. All charts share a synchronized date range so different series can be compared side by side.
- **Add, Edit & Replace Values** — Submit a date and value to add a new data point. Updating an existing date for a custom series prompts for confirmation before overwriting.
- **Date Range Filtering** — Control the display range with **From** and **To** date inputs and an **Apply** button. The range is persisted across sessions via `localStorage` and cookies.
- **Data Export (JSON)** — Download all series data as a single JSON file for backup or sharing.
- **Data Import (JSON)** — Upload a previously exported JSON file to restore data, including all series. Imported values are automatically rounded to two decimal places.
- **Clear Data** — Delete all tracked data at once (with a confirmation prompt).
- **Print-Friendly** — The **Print Chart** menu item triggers `window.print()`, hiding all interactive controls via CSS so the chart prints cleanly.
- **Responsive UI** — Built with [Bootstrap 5.3](https://getbootstrap.com/) for a clean, mobile-friendly interface.
- **Loading Spinner** — A full-screen spinner masks the page while initial Dow Jones data is being fetched.

## Technology Stack

| Component | Library / Service |
|---|---|
| UI Framework | Bootstrap 5.3 (CDN) |
| Charting | Chart.js + Chart.js Adapter Luxon |
| Date Formatting | Luxon |
| Data Fetching | Financial Modeling Prep (FMP) API (`https://financialmodelingprep.com/stable/historical-price-eod/full?symbol=^DJI&apikey=...`) |
| Persistence | `localStorage` + cookies |

## Project Structure

```
financial-tracker/
├── index.html   # Single-page application (HTML, CSS, and JavaScript bundled)
└── README.md    # This file
```

The entire application is contained in a single `index.html` file for simplicity — no build step, no server, no dependencies beyond CDN-loaded libraries. Open the file directly in a modern web browser.

## How to Run

1. Download or clone this repository.
2. Open `index.html` in a modern web browser (Chrome, Firefox, Safari, Edge).
3. On first launch, the app will automatically fetch historical Dow Jones data. A date picker modal will appear asking you to choose the **earliest date** to include — select a date and click **OK**.
4. Use the form to add new data points, create additional series, and filter the chart date range.

## API Key

The app uses a built-in API key for the Financial Modeling Prep service. To use your own key, replace the value of `FMP_API_KEY` near the top of the `<script>` block in `index.html`:

```javascript
const FMP_API_KEY = 'YOUR_API_KEY_HERE';
```

## Data Storage

All tracked data is stored in the browser's `localStorage` under the following keys:

| Key | Description |
|---|---|
| `series_list` | JSON array of all series names (Dow Jones is always included). |
| `dow_values` | Array of `{ date, value }` objects for the Dow Jones Industrial Average. |
| `series_<name>` | Array of `{ date, value }` objects for each user-defined series. |
| `chartDateRange` | Persisted chart date range (`{ from, to }`) for both `localStorage` and a cookie. |

## License

This project is provided as-is for personal or educational use.