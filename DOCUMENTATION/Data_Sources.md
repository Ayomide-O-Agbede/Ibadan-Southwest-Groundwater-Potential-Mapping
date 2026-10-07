# Data Sources

The project used the following datasets for the groundwater potential assessment.

## 1. SRTM Digital Elevation Model

* **Dataset:** SRTM 1 Arc-Second Global DEM
* **Resolution:** Approximately 30 m
* **Provider:** USGS
* **Source:** USGS EarthExplorer
* **Use:** Elevation, slope, flow accumulation and drainage-network derivation

The DEM was reprojected to **WGS 84 / UTM Zone 31N (EPSG:32631)** and clipped to the study area.

## 2. ESA WorldCover

* **Dataset:** ESA WorldCover 2021 v2.0
* **Resolution:** 10 m
* **Provider:** European Space Agency
* **Use:** Land use/land cover factor

The WorldCover raster was reprojected using **nearest-neighbour resampling**, clipped to the study area and later resampled to the project analysis grid.

## 3. CHIRPS Rainfall

* **Dataset:** CHIRPS annual rainfall
* **Period:** 2001–2025
* **Resolution:** Approximately 0.05°
* **Provider:** Climate Hazards Center, UCSB
* **Use:** Investigated as a possible groundwater-related factor

Annual rainfall data were processed to obtain a mean rainfall surface. However, CHIRPS was not included in the final weighted overlay because its spatial resolution was too coarse for the study area.

## 4. Study-Area Boundary

* **Dataset:** Ibadan Southwest LGA boundary
* **Type:** Polygon
* **Use:** Study-area definition, clipping and spatial masking

The boundary was used to standardise the extent of the analysis.

## 5. Coordinate Reference System

The main analysis used **WGS 84 / UTM Zone 31N (EPSG:32631)**.

A projected CRS was used because the analysis involved distance and terrain calculations in metres.

## Data Processing

The source datasets were processed mainly in **QGIS**, with **GRASS GIS** and **GDAL** used for specific terrain, hydrological and raster operations.

The main processing steps included reprojection, clipping, DEM processing, flow accumulation, drainage extraction, distance calculation, raster resampling and suitability reclassification.

The detailed processing workflow is documented in [`Methodology.md`](Methodology.md).
