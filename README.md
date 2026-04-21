# FuelTrack — India Route Optimizer

<p align="center">
  <svg width="320" viewBox="0 0 320 96" role="img" aria-label="FuelTrack logo with stylized fuel gauge" xmlns="http://www.w3.org/2000/svg">
    <title>FuelTrack logo with stylized fuel gauge</title>
    <defs>
      <linearGradient id="ftStroke" x1="0" y1="0" x2="1" y2="1">
        <stop offset="0%" stop-color="#fbbf24" />
        <stop offset="100%" stop-color="#ea580c" />
      </linearGradient>
      <linearGradient id="ftFill" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0%" stop-color="#fdba74" />
        <stop offset="100%" stop-color="#f59e0b" />
      </linearGradient>
    </defs>
    <rect x="4" y="4" width="88" height="88" rx="22" fill="#0b1526" stroke="#f59e0b55" stroke-width="2"/>
    <path d="M48 22c8 11 14 17 14 28 0 9-7 16-16 16s-16-7-16-16c0-7 4-12 10-19 2 5 5 8 8 9 1-5 1-10 0-18z" fill="url(#ftFill)"/>
    <path d="M30 70c7-8 15-8 23 0" fill="none" stroke="url(#ftStroke)" stroke-width="5" stroke-linecap="round"/>
    <circle cx="30" cy="70" r="3" fill="#f59e0b"/>
    <circle cx="53" cy="70" r="3" fill="#f59e0b"/>
    <text x="108" y="47" fill="#f59e0b" font-size="30" font-weight="700" font-family="'JetBrains Mono', 'DM Sans', sans-serif" letter-spacing="1.2">FUELTRACK</text>
    <text x="109" y="66" fill="#64748b" font-size="11" font-family="'DM Sans', sans-serif" letter-spacing="2.5">INDIA ROUTE OPTIMIZER</text>
  </svg>
</p>

FuelTrack is a single-page web application designed to help users estimate and optimize trip expenses across Indian routes. It combines route intelligence, city-aware fuel rates, toll estimation, vehicle profiling, trip history, fuel logging, analytics, and an in-app AI assistant in a fast, client-side interface.

Built as a standalone HTML application, FuelTrack runs directly in the browser without a backend server requirement for core functionality.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Product Modules](#product-modules)
- [How Cost Calculation Works](#how-cost-calculation-works)
- [Data Sources and Integrations](#data-sources-and-integrations)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Usage Guide](#usage-guide)
- [Operational Notes](#operational-notes)
- [Privacy and Security Notes](#privacy-and-security-notes)
- [Limitations](#limitations)
- [Troubleshooting](#troubleshooting)
- [Roadmap Suggestions](#roadmap-suggestions)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

FuelTrack helps drivers and fleet operators make more informed decisions by estimating travel costs using:

- Real or fallback route distance and duration
- Vehicle-specific mileage and toll multipliers
- Fuel-type-aware cost computation (petrol, diesel, CNG, EV)
- Known route toll pricing for selected Indian corridors
- Personal fuel log data to reuse latest city-specific rates

The app emphasizes practical utility, clear visualizations, and a clean operator-focused UI.

---

## Key Features

- **Route Planner** with step-based workflow (Locations → Fuel → Vehicle)
- **Live map rendering** for selected route with origin/destination markers
- **Distance and duration estimation** using routing APIs with fallback logic
- **Fuel cost and toll cost breakdown** with total trip projection
- **Known toll support** for curated real-world route pairs
- **Fuel Log module** to store fill-up entries and reuse latest rates
- **Dashboard** for high-level totals (spend, distance, toll, entries)
- **Analytics** with monthly trends and expense split charts
- **Vehicle catalog** including cars, two-wheelers, EVs, and commercial classes
- **AI assistant** focused on Indian fuel/toll/route domain queries

---

## Product Modules

### 1) Route Planner
The planner captures origin, destination, fuel settings, and vehicle configuration to compute a route-level estimate. It surfaces:

- Distance (km)
- Duration
- Fuel usage and fuel cost
- Toll (exact when known, estimated otherwise)
- Cost per kilometer
- Toll-route vs toll-free comparative view

### 2) Fuel Logs
Users can record refueling events with:

- Date
- City
- Fuel type
- Litres
- Price per litre
- Total amount

Latest city/fuel-type rates from logs can be reused during route planning.

### 3) Dashboard
A consolidated operational view of:

- Total spend
- Total fuel and toll components
- Distance traveled
- Active vehicle profile
- Trip history table

### 4) Analytics
Visual representations include:

- Monthly fuel/toll trend (line/area)
- Expense composition (doughnut chart)
- Monthly spend bars
- Smart insights derived from aggregate activity

### 5) AI Chat
An embedded assistant intended for fuel, route, toll, EV, and mileage-related guidance. It includes fallback responses when live AI service is unavailable.

---

## How Cost Calculation Works

At a high level, FuelTrack computes total trip cost as:

**Total = Fuel Cost + Toll Cost**

### Fuel Cost
- For ICE/CNG vehicles: based on selected mileage and effective rate
- For EVs: estimated using a fixed per-km charging approximation

### Toll Cost Priority
1. Toll API (if configured and available)
2. Known route toll table (curated route pairs)
3. Heuristic estimate for remaining routes

### Routing Priority
1. Mappls route API
2. OSRM route API
3. Straight-line fallback with scaling factor

This layered strategy keeps the app usable even during partial API unavailability.

---

## Data Sources and Integrations

FuelTrack currently integrates or references:

- **Mappls Routing API** for route distance/duration
- **OSRM** as free/open routing fallback
- **OpenStreetMap Nominatim** for geocoding and location hinting
- **TollGuru API** (optional key-based integration)
- **Google Gemini API** for AI responses
- **Leaflet** for map rendering
- **Chart.js** for analytics charts
- **ArcGIS tile services** for map imagery and labels

---

## Technology Stack

- **Frontend runtime:** Vanilla HTML, CSS, JavaScript
- **Mapping:** Leaflet + ArcGIS tiles
- **Charts:** Chart.js
- **Architecture style:** Single-file SPA (no build step required)
- **Persistence:** In-memory state during session (no dedicated backend in current implementation)

---

## Project Structure

```text
FuelTracker/
└── index.html   # Entire UI, styles, state, service calls, and rendering logic
```

The current repository is intentionally lightweight and centered around one deployable page.

---

## Getting Started

### Prerequisites

- A modern desktop browser (Chrome, Edge, Firefox, Safari)
- Internet access (for CDN assets and external API-backed features)

### Run Locally

1. Clone the repository.
2. Open `index.html` in your browser.

You can also serve it using any static file server for a more production-like local environment.

---

## Configuration

Configuration variables are defined in `index.html` under `CONFIG` and top-level constants.

### Core Config Values

- `TOLLGURU_API`
- `MAPPLS_REST_API`
- `apiKey` (Gemini API key variable)

### Notes

- Keep API keys private and do not expose real secrets in public repositories.
- If optional APIs are not configured, FuelTrack falls back to alternate logic where available.

---

## Usage Guide

### Plan a Route

1. Open **Route Planner**.
2. Enter origin and destination.
3. Choose fuel type and (optional) manual rate.
4. Select vehicle type and verify mileage.
5. Calculate route to view distance, duration, and cost breakdown.
6. Save trip to include it in dashboard/analytics.

### Log Fuel Purchase

1. Open **Fuel Logs**.
2. Enter date, city, fuel type, litres, and price/litre.
3. Save entry and review auto-generated summary and rate panels.

### Monitor Performance

- Use **Dashboard** for operational totals.
- Use **Analytics** for trends and distribution insights.
- Use **AI Chat** for guidance on route/fuel/toll decisions.

---

## Operational Notes

- Vehicle selection affects both mileage and toll multiplier assumptions.
- Some route toll values are curated and treated as “exact” for known city pairs.
- Unknown corridors use estimation heuristics and should be treated as directional planning values.
- Live routing/geocoding quality depends on network and provider availability.

---

## Privacy and Security Notes

- This app is frontend-only in its current form.
- API keys in client-side code are visible to end users; production usage should move sensitive operations server-side.
- Avoid committing real production credentials.
- Validate legal and policy constraints for third-party API usage and data storage before deployment.

---

## Limitations

- Single-file architecture can become harder to maintain at scale.
- No backend persistence layer for durable multi-user storage.
- Estimates may vary from real-world traffic, toll policy updates, and city-level fuel price fluctuations.
- AI assistant accuracy depends on upstream model/service availability.

---

## Troubleshooting

### Route not loading
- Verify internet connection.
- Check whether third-party routing endpoints are reachable.
- Retry with clearer city names.

### Fuel rate looks incorrect
- Confirm selected city/fuel type.
- Add a fresh fuel log entry for the city to override defaults.

### AI chat unavailable
- Confirm AI API key setup and network availability.
- App will use fallback responses when live generation is unavailable.

### Map appears blank or misaligned
- Refresh the page.
- Ensure browser allows remote tile/network requests.

---

## Roadmap Suggestions

Potential future enhancements:

- Modularize codebase (split CSS/JS into dedicated files)
- Add persistent storage (localStorage or backend)
- Add authentication and profile-based trip books
- Add export/reporting (CSV/PDF)
- Improve toll intelligence coverage for more route pairs
- Add unit tests and CI quality gates
- Add PWA/offline-first capability

---

## Contributing

Contributions are welcome. For high-quality pull requests:

1. Keep changes focused and scoped.
2. Preserve existing UI and calculation behavior unless intentionally changing it.
3. Document major feature additions and configuration changes.
4. Validate functionality manually in a browser before submitting.

---

## License

No license file is currently present in this repository.

If you intend to open-source this project formally, add a standard license (for example MIT, Apache-2.0, or GPL) and update this section accordingly.

---

### Maintainer Note

If you are the project owner, consider rotating and externalizing API keys before wider publication.
