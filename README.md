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
