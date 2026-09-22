# Methodology

## 1. Project Overview

This project presents a GIS-based groundwater potential assessment of Ibadan Southwest Local Government Area, Oyo State, Nigeria. The objective was to integrate selected terrain, drainage, land-use/land-cover and elevation factors in a weighted overlay to produce a relative groundwater potential index.

The assessment is intended to support groundwater exploration planning. It represents relative groundwater potential based on the selected spatial factors and does not represent measured borehole yield or groundwater productivity.

## 2. Study Area

The study area is Ibadan Southwest Local Government Area in Oyo State, southwestern Nigeria.

The study-area boundary was used to clip and standardize the spatial datasets used in the analysis.

All major analysis layers were projected to:

**WGS 84 / UTM Zone 31N (EPSG:32631)**

This projected coordinate system was used to ensure that distance and terrain-related calculations were performed in metres.

## 3. Data Sources

The main datasets used were:

- SRTM 1 Arc-Second Global (~30 m) Digital Elevation Model from USGS EarthExplorer
- ESA WorldCover 2021 v2.0 (10 m) for land use/land cover
- CHIRPS annual rainfall data for 2001–2025
- Ibadan Southwest LGA study-area boundary

CHIRPS rainfall data were investigated as a potential groundwater-related factor but were not included in the final weighted overlay because their spatial resolution was considered too coarse for detailed spatial modelling within the relatively small study area.

## 4. DEM Preprocessing

The original SRTM DEM was reprojected to WGS 84 / UTM Zone 31N (EPSG:32631) and clipped to the Ibadan Southwest study boundary.

A filled DEM was subsequently produced using the QGIS Fill Sinks (Wang & Liu) algorithm. The filled DEM was used for hydrological processing and was not used as the final elevation map.

## 5. Slope Generation

Slope was derived from the projected SRTM DEM.

The resulting slope raster had values ranging from approximately 0° to 16.22°.

For the groundwater potential assessment, slope was reclassified into five suitability classes:

| Slope | Suitability |
|---|---:|
| 0–3° | 5 |
| 3–6° | 4 |
| 6–9° | 3 |
| 9–12° | 2 |
| 12–16.22° | 1 |

Lower slopes were assigned higher suitability because flatter terrain can favour infiltration and reduce rapid surface runoff.

## 6. Drainage Network and Distance to Drainage

Flow accumulation was generated from the filled DEM using the GRASS `r.watershed` algorithm.

A threshold of 1000 was used to derive the drainage/stream network. Positive flow accumulation was used because the initial flow-accumulation output contained negative values and was therefore rejected.

A binary stream network was subsequently generated using the condition:

`Flow accumulation >= 1000`

Distance to the derived drainage network was calculated using the GDAL Proximity tool.

The resulting distance raster was clipped to the study boundary before suitability classification.

Distance to drainage was then reclassified into five suitability classes using equal-interval ranges:

| Distance to drainage | Suitability |
|---|---:|
| 0–324.72 m | 5 |
| 324.72–649.45 m | 4 |
| 649.45–974.17 m | 3 |
| 974.17–1298.89 m | 2 |
| 1298.89–1623.62 m | 1 |

Areas closer to drainage were assigned higher suitability.

## 7. Land Use/Land Cover

ESA WorldCover 2021 v2.0 was used to represent land use/land cover.

The original WorldCover raster was reprojected to EPSG:32631 using nearest-neighbour resampling and clipped to the study boundary.

The land-cover classes present within the study area included:

- Tree cover
- Shrubland
- Grassland
- Cropland
- Built-up
- Bare/sparse vegetation

The classes were assigned groundwater suitability scores based on their relative influence on infiltration and surface conditions:

| LULC class | Suitability |
|---|---:|
| Tree cover | 5 |
| Shrubland | 4 |
| Grassland | 4 |
| Cropland | 3 |
| Built-up | 1 |
| Bare/sparse vegetation | 2 |

The resulting suitability raster was resampled to the approximately 30 m analysis grid using nearest-neighbour resampling.

## 8. Elevation Suitability

Elevation was derived from the SRTM DEM and reclassified into five relative suitability classes:

| Elevation | Suitability |
|---|---:|
| 133–154 m | 5 |
| 154–174 m | 4 |
| 174–194 m | 3 |
| 194–214 m | 2 |
| 214–234 m | 1 |

Elevation was treated as a relative terrain factor rather than a direct measure of groundwater availability.

## 9. Weighted Overlay

Four factors were selected for the final groundwater potential assessment:

| Factor | Weight |
|---|---:|
| Slope | 30% |
| Distance to drainage | 30% |
| Land use/land cover | 25% |
| Elevation | 15% |

Each factor was standardized to a suitability scale from 1 (Very Low) to 5 (Very High).

The Groundwater Potential Index (GWPI) was calculated using:

`GWPI = (Slope × 0.30) + (Distance to Drainage × 0.30) + (LULC × 0.25) + (Elevation × 0.15)`

The weights represent an expert-informed weighting scheme for this portfolio assessment. They were not statistically calibrated because spatial borehole validation data were not available for the study.

## 10. Groundwater Potential Classification

The final GWPI is a continuous raster with values ranging approximately from 1.30 to 5.00.

For map interpretation, the continuous index was displayed using five classes:

- Very Low
- Low
- Moderate
- High
- Very High

These classes are cartographic interpretation classes applied to the continuous index and do not represent measured groundwater yield categories.

## 11. Map Production

Six thematic maps were produced:

1. Study Area Map
2. Elevation Map
3. Slope Map
4. Distance to Drainage Map
5. Land Use/Land Cover Map
6. Groundwater Potential Map

Each map includes appropriate map elements such as a title, legend, north arrow, scale bar, coordinate reference system and data-source information.

## 12. Software

The analysis was carried out primarily in QGIS 3.44.9, using GDAL and GRASS GIS processing tools available within the QGIS environment.