# Groundwater Potential Mapping of Ibadan Southwest LGA, Oyo State, Nigeria

## Project Overview

This project presents a GIS-based groundwater potential assessment of Ibadan Southwest Local Government Area, Oyo State, Nigeria.

The assessment integrates terrain, drainage, land use/land cover and elevation data to produce a relative groundwater potential index. The project was developed in QGIS as a practical geospatial workflow for supporting groundwater exploration and water-resources planning.

The final model combines four factors using an expert-informed weighted overlay:

| Factor               | Weight |
| -------------------- | -----: |
| Slope                |    30% |
| Distance to drainage |    30% |
| Land use/land cover  |    25% |
| Elevation            |    15% |

The resulting map identifies areas with relatively higher or lower groundwater potential based on the selected spatial factors.

## Objectives

* Prepare and integrate publicly available geospatial datasets for groundwater assessment.
* Derive terrain and drainage-related factors from a digital elevation model.
* Assess the influence of land use/land cover and elevation on relative groundwater potential.
* Apply a weighted overlay model to generate a groundwater potential index.
* Produce clear thematic maps for groundwater exploration planning.
* Document the complete GIS processing workflow, including corrections and limitations encountered during analysis.

## Study Area

The study focuses on **Ibadan Southwest Local Government Area in Oyo State, Nigeria**.

All major spatial analysis was carried out using **WGS 84 / UTM Zone 31N (EPSG:32631)** to support distance and terrain-based calculations in metres.

## Data Sources

The project used the following datasets:

* **SRTM 1 Arc-Second Global DEM (~30 m)** — USGS EarthExplorer
* **ESA WorldCover 2021 v2.0 (10 m)** — European Space Agency
* **CHIRPS annual rainfall data (2001–2025)** — Climate Hazards Center, UCSB
* **Ibadan Southwest LGA boundary** — study-area boundary dataset

Detailed information about the datasets and their sources is available in [`DOCUMENTATION/Data_Sources.md`](DOCUMENTATION/Data_Sources.md).

## Methodology

The main workflow consisted of:

1. Preparing the study-area boundary and coordinate reference system.
2. Reprojecting and clipping the SRTM DEM.
3. Deriving slope from the projected DEM.
4. Filling DEM sinks for hydrological processing.
5. Generating flow accumulation using GRASS GIS.
6. Extracting a drainage network using a flow-accumulation threshold of 1000.
7. Calculating distance to the derived drainage network.
8. Processing and classifying ESA WorldCover land use/land cover data.
9. Reclassifying the selected factors into suitability scores from 1 to 5.
10. Resampling the LULC suitability layer to match the analysis grid.
11. Combining the four factors using the weighted overlay equation.
12. Producing the final groundwater potential index and thematic maps.

The detailed methodology is provided in [`DOCUMENTATION/Methodology.md`](DOCUMENTATION/Methodology.md).

## Groundwater Potential Model

The final groundwater potential index was calculated as:

```text
GWPI =
(Slope Suitability × 0.30)
+
(Distance to Drainage Suitability × 0.30)
+
(LULC Suitability × 0.25)
+
(Elevation Suitability × 0.15)
```

The resulting continuous index was classified for map presentation into five relative potential classes:

* Very Low
* Low
* Moderate
* High
* Very High

The final GWPI raster has values ranging from approximately **1.30 to 5.00**.

## Final Maps

The project produced six thematic maps:

### 01 — Study Area Map

Shows the location and spatial extent of the Ibadan Southwest study area.

### 02 — Elevation Map

Shows the elevation pattern derived from the SRTM DEM.

### 03 — Slope Map

Shows terrain slope across the study area.

### 04 — Distance to Drainage Map

Shows the distance of locations from the derived drainage network.

### 05 — Land Use/Land Cover Map

Shows the 2021 ESA WorldCover classes within the study area.

### 06 — Groundwater Potential Map

Shows the final relative groundwater potential index generated from the weighted overlay model.

The maps are available in [`OUTPUTS/MAPS`](OUTPUTS/MAPS).

## Results

The final groundwater potential index produced a continuous range of approximately **1.30–5.00**.

The model integrates:

* terrain steepness,
* proximity to drainage,
* land use/land cover, and
* relative elevation.

The resulting map provides a spatial representation of relative groundwater potential that can be used to identify areas for further investigation and groundwater exploration planning.

The final raster is available in [`OUTPUTS/RASTERS`](OUTPUTS/RASTERS).

## Processing Notes

The project included several processing corrections during development.

For example, the initial slope calculation was identified as unsuitable because the DEM was processed in a geographic coordinate system. The DEM was subsequently projected to UTM Zone 31N and the slope was recalculated.

The initial flow-accumulation output also contained negative values. A corrected flow-accumulation workflow was therefore implemented before deriving the drainage network.

Distance-to-drainage suitability was recalculated after clipping the distance raster to the study boundary to ensure that the classification represented the actual study area.

CHIRPS rainfall data were investigated as a potential factor. However, the rainfall dataset was excluded from the final weighted overlay because its spatial resolution was considered too coarse for detailed modelling within the relatively small study area.

These and other processing decisions are documented in [`DOCUMENTATION/Processing_Notes.md`](DOCUMENTATION/Processing_Notes.md).

## Limitations

This assessment represents **relative groundwater potential**, not measured groundwater yield.

The final model was not statistically validated against spatial borehole-yield data. The factor weights were therefore **expert-informed weights developed for this portfolio assessment** rather than statistically calibrated weights.

Other factors that can influence groundwater occurrence, such as detailed geology, aquifer properties and borehole observations, were not included in the final weighted overlay.

The results should therefore be considered a **screening and exploration-planning tool** rather than a substitute for detailed hydrogeological investigation, geophysical surveys or borehole testing.

## Software

* QGIS 3.44.9
* GRASS GIS
* GDAL
* ESA WorldCover
* SRTM
* CHIRPS

## Project Structure

```text
Ibadan-Southwest-Groundwater-Potential-Mapping/
│
├── README.md
│
├── MAPS/
│   ├── 01_Study_Area_Map.png
│   ├── 02_Elevation_Map.png
│   ├── 03_Slope_Map.png
│   ├── 04_Distance_to_Drainage_Map.png
│   ├── 05_Land_Use_Land_Cover_Map.png
│   └── 06_Groundwater_Potential_Map.png
│
├── RASTERS/
│   └── Ibadan_Southwest_Groundwater_Potential_Index_v2.tif
│
└── DOCUMENTATION/
    ├── Methodology.md
    ├── Processing_Notes.md
    └── Data_Sources.md
```

## Author

**Ayomide Odunayo Agbede**

Hydrogeophysicist | GIS & Remote Sensing | Water Resources

Nigeria
