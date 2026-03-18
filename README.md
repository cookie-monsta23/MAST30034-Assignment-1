# Assignment 1: NYC Taxi Congestion Analysis and Forecasting

**Student:** Venura De Alwis  

## Overview

This repository contains an end-to-end data science workflow for analyzing New York City taxi congestion patterns and forecasting congestion-related indicators. The analysis is implemented in a single notebook that combines:

- large-scale trip processing with PySpark,
- data quality filtering and outlier handling,
- zone-level congestion feature engineering,
- geospatial visualization with shapefiles and Folium,
- supervised machine learning for multi-output prediction.

The project focuses on yellow and green taxi trip data, with weather and zone geometry features integrated for richer modeling.

## Project Objectives

1. Build a clean and defensible trip-level dataset from raw taxi files.
2. Derive congestion-oriented measures from travel time and distance.
3. Aggregate daily/zone metrics and identify high-congestion locations.
4. Visualize zone-level congestion patterns spatially.
5. Train and compare forecasting-style regression models for key outputs.

## Repository Structure

```text
.
├── README.md
├── requirements.txt
├── notebooks/
│   └── Assignment_1.ipynb
├── plots/
│   ├── foliumChoroplethMap1.html
│   └── foliumChoroplethMap2.html
├── taxi_data/
│   ├── green/
│   │   ├── 2023/
│   │   ├── 2024/
│   │   └── 2025/
│   ├── irregular/
│   └── yellow/
│       ├── 2023/
│       ├── 2024/
│       └── 2025/
└── taxi_data_2/
    ├── 2023and2024 Weather.csv
    ├── 2025 Weather.csv
    └── taxi_zones/
        ├── taxi_zone_lookup.csv
        ├── taxi_zones.dbf
        ├── taxi_zones.prj
        ├── taxi_zones.sbn
        ├── taxi_zones.sbx
        ├── taxi_zones.shp
        ├── taxi_zones.shp.xml
        └── taxi_zones.shx
```

## Data Notes

- `taxi_data/` holds downloaded and generated trip parquet files used during processing.
- `taxi_data_2/` contains custom-range weather data and taxi zone geometry/lookup resources used by the notebook.
- `plots/` stores HTML map outputs exported by Folium.

## Methodology Summary

The notebook workflow includes:

1. **Ingestion and setup**
   - Creates Spark session.
   - Loads trip data and supporting files.
2. **Data cleaning and filtering**
   - Removes invalid/null records.
   - Applies domain-based filters for trip time, distance, and fare validity.
   - Applies outlier treatment logic.
3. **Congestion metric derivation**
   - Estimates expected vs observed travel behavior.
   - Builds congestion-time style features.
4. **Aggregation and exploratory analysis**
   - Computes zone-level and date-level statistics.
   - Identifies high-congestion zones.
5. **Geospatial visualization**
   - Joins metrics with NYC taxi zone geometries.
   - Produces choropleth HTML maps.
6. **Modeling**
   - Engineers lag/rolling features and weather features.
   - Trains and evaluates multiple regression approaches, including XGBoost and multi-output models.

## Environment Setup

### Prerequisites

- Python 3.10+
- Java runtime available for PySpark

### Install dependencies

```bash
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

## Running the Project

1. Open `notebooks/Assignment_1.ipynb`.
2. Select the Python environment where requirements are installed.
3. Run cells top-to-bottom.
4. Review generated map outputs under `plots/`.

## Reproducibility and Refactor Notes

- `requirements.txt` is aligned with packages imported in the notebook.
- `.gitignore` is configured for Python, Jupyter, Spark, and macOS artifacts.
- Local-generated parquet data in `taxi_data/` remains excluded from version control.

## Troubleshooting

- **PySpark fails to initialize**: verify Java is installed and accessible in your shell.
- **Memory pressure in notebook**: run sections incrementally or sample data for exploratory runs.
- **Map rendering issues**: ensure `geopandas` and `folium` are correctly installed in the active environment.

## Acknowledgements

- NYC Taxi and Limousine Commission trip data resources.
- Open-source Python ecosystem: PySpark, scikit-learn, XGBoost, GeoPandas, and Folium.
