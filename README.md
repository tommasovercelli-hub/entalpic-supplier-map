# Entalpic — Global Precursor Supplier Map

Interactive map of 74 HQ / Plant / R&D sites across 13 precursor-supplier
parent companies. Built on Leaflet + OpenStreetMap, no API key, no build step.

## Files

- `index.html` — the map UI
- `suppliers.csv` — the data (74 rows, edit freely)
- `geocodes.json` — city → lat/lon lookup (47 cities)

## Running it

Browsers block `fetch()` on `file://` URLs, so double-clicking `index.html`
won't work. Serve the folder locally:

```bash
cd precursor-map
python3 -m http.server 8000
# then open http://localhost:8000
```

## Map legend

| Marker | Meaning |
| --- | --- |
| 🔵 Blue | HQ (with gold halo — larger marker) |
| 🟠 Orange | Plant |
| 🟢 Green | R&D |
| 🟣 Purple | Plant/R&D |

The **flag** in the popup reflects the parent company's country of origin
(Air Liquide = 🇫🇷 even in Kaohsiung). The marker's **location** is the
physical site. Sites sharing a city are nudged ~1.5 km apart so each stays
clickable.

## Controls

- **Search box** — matches company, site, city, or country
- **Site type** — toggle HQ / Plant / R&D / Plant/R&D
- **Company** — toggle any of the 13 parents individually, or "toggle all"
- Live stat cards at top: visible sites / companies / countries

## CSV schema

| Column | Values |
| --- | --- |
| `flag` | Emoji flag of parent company's HQ country |
| `parent_company` | Free text |
| `site_name` | Free text |
| `city` | Must also exist as a key in `geocodes.json` |
| `country` | Free text |
| `type` | `HQ` · `Plant` · `R&D` · `Plant/R&D` |

## Adding new cities

If you add a row with a city not in `geocodes.json`, the row will be silently
skipped (with a warning in the browser console). To add a city:

1. Find its lat/lon — right-click on Google Maps, top entry in the menu is
   decimal coordinates, click to copy.
2. Add an entry to `geocodes.json`:
   ```json
   "CityName|Country": [lat, lon]
   ```
   The key format is `city|country` joined by a pipe.

## Current data summary

- 74 sites across 13 parent companies, 9 countries
- By type: 13 HQ · 33 Plant · 18 R&D · 10 Plant/R&D
- By country: South Korea 26 · USA 14 · Japan 14 · Taiwan 9 · Germany/China/France/Singapore/UK in single digits
