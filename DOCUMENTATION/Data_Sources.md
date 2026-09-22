# Data Sources

This project used publicly available geospatial datasets for the GIS-based groundwater potential assessment of Ibadan Southwest Local Government Area, Oyo State, Nigeria.

## 1. SRTM Digital Elevation Model

**Dataset:** SRTM 1 Arc-Second Global Digital Elevation Model
**Approximate spatial resolution:** 30 m
**Provider:** U.S. Geological Survey (USGS)
**Access:** USGS EarthExplorer
**Use in project:** Elevation, slope, flow accumulation and drainage-network derivation.

The DEM was reprojected to WGS 84 / UTM Zone 31N (EPSG:32631) and clipped to the study boundary.

## 2. ESA WorldCover

**Dataset:** ESA WorldCover 2021 v2.0
**Spatial resolution:** 10 m
**Provider:** European Space Agency (ESA)
**Use in project:** Land use/land cover classification and groundwater suitability assessment.

The original WorldCover raster was reprojected using nearest-neighbour resampling and clipped to the study area.

Official data access:
https://esa-worldcover.org/en/data-access

## 3. CHIRPS Rainfall

**Dataset:** Climate Hazards Center InfraRed Precipitation with Station data (CHIRPS)
**Period used:** 2001–2025
**Temporal unit:** Annual rainfall
**Approximate spatial resolution:** 0.05°
**Provider:** Climate Hazards Center, University of California, Santa Barbara
**Use in project:** Investigated as a potential supporting groundwater-related factor.

A 2001–2025 mean annual rainfall surface was calculated. However, rainfall was excluded from the final groundwater potential overlay because its spatial resolution was considered too coarse for detailed modelling within the relatively small study area.

Official data repository:
https://data.chc.ucsb.edu/products/CHIRPS/v3.0/

## 4. Study-Area Boundary

**Dataset:** Ibadan Southwest Local Government Area boundary
**Source:** Study-area boundary dataset used for the project
**Geometry:** Polygon
**Coordinate Reference System:** WGS 84 / UTM Zone 31N (EPSG:32631)
**Use in project:** Definition of the study extent and clipping of spatial datasets.

## 5. Coordinate Reference System

The principal analysis was carried out using:

**WGS 84 / UTM Zone 31N — EPSG:32631**

The projected CRS was selected to support distance and terrain-related spatial analysis in metres.

## 6. Data Processing

The source datasets were processed in QGIS before integration. Processing included reprojection, clipping, terrain analysis, hydrological processing, raster reclassification and resampling where required.

The final groundwater potential model used four factors:

* Slope — 30%
* Distance to drainage — 30%
* Land use/land cover — 25%
* Elevation — 15%

The weights were expert-informed for this portfolio assessment and were not statistically calibrated against spatial borehole yield data.
