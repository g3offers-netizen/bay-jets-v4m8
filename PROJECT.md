# Bay Area Private Jet Tracker

**Project Reference Name:** `bay-jets`
**Created:** 2026-02-08
**Live URL:** https://g3offers-netizen.github.io/bay-jets-v4m8/
**Repository:** https://github.com/g3offers-netizen/bay-jets-v4m8

---

## Overview

Real-time tracker for private jets departing/arriving at SFO, SJC, and OAK airports. Shows aircraft details, owner research, and "likely passenger" speculation.

## Features

- **Live Aircraft Data** — Updates every ~5 minutes via heartbeat
- **Owner Research** — 29+ jets with verified ownership info
- **Likely Passenger** — Speculation on who's flying based on ownership
- **Planespotters Integration** — Serial numbers, delivery dates, verified badges
- **Dark Theme** — Matches Lee's other dashboards (#1a1a2e)

## Data Sources

1. **adsb.lol API** — Free ADS-B aggregator, no CORS issues
   - Endpoint: `https://api.adsb.lol/v2/lat/37.55/lon/-122.2/dist/50`
   - Returns all aircraft within 50nm of Bay Area center

2. **FAA Registry** — Official N-number registration lookup
   - URL: `https://registry.faa.gov/AircraftInquiry/Search/NNumberResult?nNumberTxt=XXXXX`

3. **Planespotters.net** — Aircraft photos, serial numbers, operator info
   - Often shows owner/operator that FAA registry hides behind trusts

4. **Manual Research** — News articles, SEC filings, aviation forums, social media

## Files

```
/Users/lp1/clawd/bay-jets/
├── index.html          # Main dashboard (single-page app)
├── data.json           # Live aircraft data (updated by heartbeat)
├── owners.json         # Ownership research database
├── update-data.sh      # Script to fetch fresh data and push to GitHub
├── PROJECT.md          # This file
├── README.md           # GitHub readme
└── .github/
    └── workflows/
        └── update-data.yml  # GitHub Actions (backup, unreliable)
```

## Ownership Database Schema (owners.json)

```json
{
  "N3546": {
    "registered": "Nike Inc",
    "principal": "Phil Knight",
    "title": "Co-founder & Chairman Emeritus, Nike",
    "profile": "Born 1938, Portland native. Stanford MBA...",
    "likelyPassenger": "Phil Knight, CEO Elliott Hill, or Nike executive team",
    "confidence": "high",
    "verified": true,
    "serialNumber": "6346",
    "deliveryDate": "Oct 2020",
    "previousReg": null,
    "sources": ["planespotters", "news"]
  }
}
```

## Notable Owners Found

| Tail | Aircraft | Owner | Notes |
|------|----------|-------|-------|
| N459BL | G650ER | **Bill Gates** | Delivered Feb 2025 |
| N121CL | Global 7500 | **Clearlake Capital** | $80B PE firm |
| N3546 | G650ER | **Nike / Phil Knight** | Portland OR |
| N8VB | Global Express | **CBS / Shari Redstone** | Media |
| N824SS | G650ER | **Liberty Mutual** | New 2024 |
| N107TD | G-IV | **Jim Irsay** | Colts owner |
| N766GD | G600 | **MESOS ONE LLC** | Tech founder? |
| N90LE | Global Express | **ESTEIN AVIATION** | New Dec 2025 |

## Trust Structures Identified

Many jets hidden behind privacy trusts:
- **Bank of Utah Trustee** — N721KJ, N7508, N214WT, N530JW
- **TVPX Aircraft Solutions** — N121CL, N378LT (Utah trusts)
- **Wilmington Trust** — N726BF (Delaware)

## How Data Updates Work

1. **Heartbeat (every ~5 min)** — Gigi runs `/Users/lp1/clawd/bay-jets/update-data.sh`
2. Script fetches from adsb.lol API
3. Saves to data.json
4. Commits and pushes to GitHub
5. GitHub Pages serves updated file
6. Dashboard fetches data.json with cache-busting

## CORS Solution

Initial attempt used ADS-B Exchange directly — blocked by CORS.
GitHub Actions cron was unreliable (delayed hours).

**Final solution:** Local update script run during heartbeat, pushes to GitHub Pages.

## Aircraft Type Filters

Dashboard filters for private jet types:
- **Gulfstream:** GLF4, GLF5, GLF6, G280, GALX
- **Global/Challenger:** GLEX, GL5T, GL7T, CL30, CL35, CL60, CL65
- **Falcon:** F900, F2TH, FA7X, FA8X
- **Citation:** C25, C56, C68
- **Embraer:** E35, E50, E55
- **Learjet:** LJ45, LJ60

## Future Enhancements

- [ ] Historical flight tracking
- [ ] Notification when specific jets depart
- [ ] More Planespotters scraping (rate limited)
- [ ] Flight path visualization
- [ ] Owner net worth integration

## Commands

```bash
# Update data manually
/Users/lp1/clawd/bay-jets/update-data.sh

# View current jets
cat /Users/lp1/clawd/bay-jets/data.json | jq '.ac | length'

# View owners database
cat /Users/lp1/clawd/bay-jets/owners.json | jq 'keys | length'
```

## Maintenance

- **HEARTBEAT.md** includes bay-jets update
- Data refreshes every heartbeat (~5 min)
- owners.json is manually curated — add new research as jets appear
- Planespotters may CAPTCHA after ~10 searches

---

*Project created by Gigi for Lee, 2026-02-08*
