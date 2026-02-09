# Bay Area Private Jet Tracker ✈️

Real-time tracking of private jets departing from Bay Area airports (SFO, SJC, OAK).

## Live Dashboard

**🔗 https://g3offers-netizen.github.io/bay-jets-v4m8/**

## Features

- **Monitors three airports:** SFO, SJC, OAK with configurable radius
- **Filters for private jet types:**
  - Gulfstream (GLF4, GLF5, GLF6, G280, GALX, etc.)
  - Global/Challenger (GLEX, GL5T, GL7T, CL30, CL35, CL60, CL65)
  - Falcon (F900, F2TH, FA7X, FA8X)
  - Citation (C25, C56, C68, C750, etc.)
  - Embraer (E35L, E50P, E55P, etc.)
- **Shows:** Tail number, aircraft type, owner, altitude, speed, heading
- **LADD Status:** Flags aircraft on FAA's LADD (Limiting Aircraft Data Displayed) list
- **Auto-refresh:** Every 30 seconds
- **Dark theme:** Matches other dashboards (#1a1a2e)

## Data Source

Data from [ADS-B Exchange](https://globe.adsbexchange.com) - they display all aircraft regardless of FAA LADD blocking.

## CORS Workarounds

ADS-B Exchange blocks direct browser requests (CORS). Choose one of these solutions:

### Option 1: Chrome Extension (Easiest)
Install [Allow CORS: Access-Control-Allow-Origin](https://chrome.google.com/webstore/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf) and enable it on the dashboard page.

### Option 2: Local CORS Proxy
```bash
npx local-cors-proxy --proxyUrl https://globe.adsbexchange.com --port 8010
```
Then modify the dashboard to use `http://localhost:8010/proxy` as the base URL.

### Option 3: Demo Mode
Click "Load Demo Data" on the dashboard to see how it works with sample data.

### Option 4: Run Locally with Browser CORS Disabled
```bash
# macOS Chrome
open -na "Google Chrome" --args --disable-web-security --user-data-dir=/tmp/chrome-cors

# Then navigate to the local file
```

## External Links

Each aircraft card includes:
- **📸 Planespotters:** Photos and registration history
- **📋 FAA Registry:** Official registration details
- **🗺️ Track:** Live tracking on ADS-B Exchange

## Keyboard Shortcuts

- `R` - Refresh data
- `Esc` - Close detail modal

---

Built with ❤️ for tracking the Bay Area's finest wings.
