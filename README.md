# Paris_smartcity_urban_mobility_data_analytics_engineering_ml_powerbi_lakehouse


# Paris Smart City: Urban Mobility Data Analytics, Engineering, ML & Lakehouse

## Project Overview
An end-to-end geospatial data engineering and machine learning pipeline designed to analyze, model, and forecast urban mobility across Paris. Built on Databricks using the Medallion Architecture (Bronze, Silver, Gold), this project integrates open urban datasets, GIS spatial analytics, time-series forecasting, and interactive business intelligence to support smart city infrastructure planning and public decision-making.

## Architecture & Data Pipeline
The data platform follows a structured Medallion Lakehouse architecture on Databricks:

* **Bronze Layer (Raw Ingestion):** Automated ingestion of raw batch datasets from Open Data Paris, including bike-sharing (Velib) station telemetry, road traffic counters (Rue de Rivoli, Rue d'Amsterdam, Quai de Jemmapes, Boulevard Montmartre), and urban roadwork disruptions.
* **Silver Layer (Cleaned & Enriched):** Data cleansing, standardization, schema enforcement, and coordinate reference system transformations (converting between WGS84 `EPSG:4326` and Lambert-93 `EPSG:2154`). Execution of Spatial SQL operations (`ST_Buffer`, `ST_Distance`, `ST_DWithin`, `ST_Area`, `ST_Centroid`) to link road disruptions and spatial catchments with mobility flows.
* **Gold Layer (Curated Analytics & ML Ready):** Star-schema dimensional modeling and feature engineering aggregated for business intelligence reporting, digital twin visualization, and predictive modeling.

## Key Features
* **Geospatial Engineering & GIS:** Spatial catchment analysis, buffer generation around urban infrastructure, and proximity modeling using Databricks Spatial SQL, GeoPandas, and QGIS.
* **Time-Series Traffic Forecasting:** Predictive machine learning pipeline utilizing Scikit-Learn (`RandomForestRegressor`) and Holt-Winters Exponential Smoothing to project daily urban transport volumes and identify congestion bottlenecks.
* **Digital Twin & 3D Visualization:** Integration of spatial outputs with CesiumJS and BIM/CAD workflows for 3D territorial visualization.
* **Executive BI Dashboards:** Power BI reporting layer featuring DAX measures and spatial maps to monitor urban KPIs, corridor saturation, and infrastructure utilization.

## Tech Stack
* **Cloud & Lakehouse:** Databricks, Apache Spark, Delta Lake
* **Languages & Libraries:** Python, PySpark, SQL, Spatial SQL, Pandas, GeoPandas, Scikit-Learn, Statsmodels
* **GIS & 3D Modeling:** QGIS, PostGIS, CesiumJS
* **Business Intelligence:** Power BI (DAX, Power Query)

# Methodology

## 1. Spatial Data Engineering & CRS Standardization
Urban datasets originate in heterogeneous formats and coordinate systems. Geographic coordinates (`EPSG:4326`) are systematically reprojected into the French planar metric projection (`EPSG:2154` / RGF93 - Lambert-93). This guarantees metric precision when computing polygon areas (`ST_Area`), infrastructure catchment buffers (`ST_Buffer`), and proximity thresholds (`ST_DWithin`) between roadworks and transit corridors.

## 2. Medallion Lakehouse Governance
Data progresses through strict quality gates. The Bronze layer preserves raw state history in Delta format. The Silver layer applies deduplication, handles missing sensor telemetry, and performs spatial joins. The Gold layer structures data into an analytical star schema optimized for fast BI querying and ML feature consumption.

## 3. Time-Series & Spatial Machine Learning
Forecasting urban mobility requires capturing both temporal seasonality and spatial disruptions. The modeling approach combines statistical baseline models (Holt-Winters Exponential Smoothing) to capture weekly and seasonal commuting cycles with tree-based ensemble regressors (`RandomForestRegressor`) trained on engineered lag features, calendar events, and active construction zone indicators.

# Workflow

1. **Data Extraction & Bronze Ingestion:** Ingest Open Data Paris datasets (traffic counts, Velib stations, construction perimeters) into Databricks DBFS and register raw Bronze Delta tables.
2. **Silver Cleaning & Spatial ETL:** Filter invalid sensor logs, standardize timestamps, transform geometries from `EPSG:4326` to `EPSG:2154`, and run Spatial SQL queries to quantify the impact of road disruptions within a defined meter radius of major corridors.
3. **Gold Dimensional Aggregation:** Aggregate hourly and daily mobility metrics by corridor and district, building curated Gold tables for analytics and machine learning.
4. **Model Training & Forecasting:** Execute feature engineering on Gold time-series data, train the Holt-Winters and Random Forest models, validate performance metrics (MAE, RMSE), and generate daily traffic projections.
5. **BI & Digital Twin Deployment:** Connect Power BI to Gold tables to track urban mobility KPIs, and export spatial layers to QGIS and CesiumJS for 3D digital twin visualization.
