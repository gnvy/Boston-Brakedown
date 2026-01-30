# Boston Cycling Safety & Traffic Visualization


<img width="1376" height="769" alt="Screenshot 2026-01-29 at 7 11 01 PM" src="https://github.com/user-attachments/assets/25017e14-3e0c-456a-ba8f-ed4e3a897eab" />

## Project Overview
This project develops an interactive, data-driven map for cyclists in Boston, visualizing road safety and bike traffic patterns using open-source data. The map provides a street-level view of cycling risk based on crash reports, potholes, theft incidents, and Bluebikes trip data, helping cyclists make safer and more informed route choices.

## Data Sources
All data is publicly available and hosted by the City of Boston or relevant agencies:

- **Boston 311 Service Data** – Unresolved pothole reports (daily updates)
- **Vision Zero Crash Data** – Bicycle-involved crashes (2015–present)
- **BPD Crime Incident Reports** – Bicycle theft incidents (2023–present)
- **Bluebikes System Data** – Trip records (Nov 2024 – Nov 2025)
- **Weather Data** – Daily temperature and precipitation (scraped from NWS)
- **OpenStreetMap (OSM)** – Street geometry
- **CartoDB Voyager** – Base map layer

## Methodology

### Data Processing
- Python pipelines using Pandas for ETL (Extract, Transform, Load)
- Data stored and processed via AWS S3
- Filtering applied to isolate relevant records:
  - Pothole cases from 311 data
  - Bike crashes from Vision Zero
  - Bike thefts from BPD reports
- Bluebikes data aggregated into:
  - Total trips by date
  - Station popularity
  - Route popularity

### Risk Scoring Algorithm
Each street segment is assigned a composite risk score calculated as:

_Risk Level = (Crash Count × 100) + (Theft Count × 20) + (Pothole Count × 5)_

Crashes are weighted most heavily to reflect safety priority.

### Visualization
- Built with **Folium** in Python
- Overlay layers for potholes, crashes, thefts, and risk scores
- Color gradients used to represent risk levels on street segments
- Pop-up windows display relevant attributes per data point

## Key Findings
- High-risk streets align with known dangerous corridors (e.g., Storrow Drive, JFK Expressway)
- Bike traffic is concentrated around MIT, partly due to the Valet station
- Temperature positively correlates with ridership; precipitation analysis was limited by data granularity

## How to Run the Code
Navigate to the `maps/` folder and open one of the following HTML files in your browser:

`boston_bike_map.html` – Displays aggregated street risk factors with safety coloring (crashes, thefts, potholes)
`boston_top_routes.html` – Shows bike traffic visualization based on top Bluebikes routes
