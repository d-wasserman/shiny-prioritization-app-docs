# GeoJSON Prioritization App

A [Shiny for Python](https://shiny.posit.co/py/) web app for interactive geospatial prioritization. Upload a GeoJSON file, adjust weights for any scoring fields, and instantly see a color-coded map of prioritized features. Download the result with the calculated score embedded.

![Demo](assets/Prioritization_Shiny_App_Demo.gif)

---

## Features

- **Dynamic weight sliders** — automatically generated for any column ending in `_SCORE`
- **Interactive map** — dark-themed Leaflet map with tooltips showing prioritization scores
- **Quantile-based classification** — configurable 2–10 class breaks
- **Multiple color ramps** — Viridis, Plasma, Inferno, Magma, Cividis, YlOrRd, YlGnBu, RdYlGn, Blues, Reds, Cool-Warm
- **Auto-fit viewport** — map zooms to the bounding box of the loaded data
- **Download result** — export scored GeoJSON with the `Prioritization` field included
- **Built-in sample data** — loads a Salt Lake Valley example on startup; no upload required to explore

---

## Getting Started

### Prerequisites

- Python 3.9+

### Installation

```bash
pip install shiny pandas matplotlib pytest
```

### Run the App

```bash
# Standard
shiny run app.py

# With auto-reload during development
shiny run app.py --reload
```

Then open `http://127.0.0.1:8000` in your browser.

---

## Usage

1. **Upload a GeoJSON file** (or use the built-in sample data).
2. **Adjust the weight sliders** for each `_SCORE` field — weights are normalized to sum to 1 automatically.
3. **Configure the map display** using the controls bar at the bottom:
   - *Classes* — number of quantile breaks (2–10)
   - *Color Ramp* — matplotlib colormap to apply
4. **Explore the map** — hover over features to see the `Prioritization` score tooltip.
5. **Download** the scored GeoJSON via the orange button in the sidebar.

---

## GeoJSON Format

The app auto-detects prioritization inputs from your GeoJSON properties. Any column ending in `_SCORE` (case-insensitive) becomes a slider.

**Example properties:**

```json
{
  "ID": 1,
  "Safety_SCORE": 4.2,
  "Connectivity_SCORE": 3.1,
  "Other_Field": "Some label"
}
```

The output adds a `Prioritization` field — the normalized weighted sum of all `_SCORE` columns.

---

## Sample Data

| File | Description |
|---|---|
| `data/Sample.geojson` | Built-in 3-feature line example (Salt Lake Valley) |
| `data/WestValleyATPNetwork.geojson` | West Valley active transportation network |
| `data/BSTPrioritization_122225.geojson` | ~6.4 MB polygon dataset for stress testing |

---

## Dependencies

| Package | Purpose |
|---|---|
| `shiny` | Web framework |
| `pandas` | DataFrame operations |
| `matplotlib` | Colormap sampling |
| `pytest` | Testing |

> **Note:** `shinywidgets` is **not** used. Pydeck 0.9 removed ipywidgets support; the map is rendered as a plain HTML iframe using Leaflet.

---

## License

GNU
