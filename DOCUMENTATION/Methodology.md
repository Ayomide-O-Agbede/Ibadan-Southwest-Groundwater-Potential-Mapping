# Methodology

## 1. Study Area and CRS

The assessment was carried out in **Ibadan Southwest Local Government Area, Oyo State, Nigeria**.

The main analysis used **WGS 84 / UTM Zone 31N (EPSG:32631)**. The projected CRS was used for terrain and distance calculations in metres.

## 2. DEM Processing

The SRTM DEM was reprojected to EPSG:32631 and clipped to the study area.

A filled DEM was then generated using the **QGIS Fill Sinks (Wang & Liu)** tool. The filled DEM was used for hydrological processing, while the original projected DEM was used for the elevation and slope analysis.

## 3. Slope

Slope was derived from the projected DEM. The resulting slope values ranged from approximately **0 to 16.22°**.

The slope was reclassified into five suitability classes:

| Slope (°) | Suitability |
| --------: | ----------: |
|       0–3 |           5 |
|       3–6 |           4 |
|       6–9 |           3 |
|      9–12 |           2 |
|  12–16.22 |           1 |

Lower slopes were given higher suitability because flatter areas can favour infiltration and reduce rapid surface runoff.

## 4. Flow Accumulation and Drainage

Flow accumulation was generated from the filled DEM using the **GRASS GIS `r.watershed`** tool.

An initial flow-accumulation output contained negative values and was rejected. The corrected positive flow-accumulation output was used for drainage extraction.

A threshold of **1000** was used to extract the drainage network.

Distance to the derived drainage network was calculated using **GDAL Proximity** and clipped to the study-area boundary.

The distance raster was reclassified as follows:

| Distance to Drainage (m) | Suitability |
| -----------------------: | ----------: |
|                 0–324.72 |           5 |
|            324.72–649.45 |           4 |
|            649.45–974.17 |           3 |
|           974.17–1298.89 |           2 |
|          1298.89–1623.62 |           1 |

Areas closer to the drainage network were given higher suitability.

## 5. Land Use/Land Cover

ESA WorldCover 2021 v2.0 was used as the LULC dataset.

The raster was reprojected using **nearest-neighbour resampling**, clipped to the study area and reclassified to a 1–5 suitability scale.

| WorldCover Class       | Suitability |
| ---------------------- | ----------: |
| Tree cover             |           5 |
| Shrubland              |           4 |
| Grassland              |           4 |
| Cropland               |           3 |
| Bare/sparse vegetation |           2 |
| Built-up               |           1 |

The 10 m LULC raster was later resampled to approximately the 30 m analysis grid using nearest-neighbour resampling.

## 6. Elevation

Elevation values in the study area ranged from approximately **133 to 234 m**.

The elevation factor was reclassified as follows:

| Elevation (m) | Suitability |
| ------------: | ----------: |
|       133–154 |           5 |
|       154–174 |           4 |
|       174–194 |           3 |
|       194–214 |           2 |
|       214–234 |           1 |

Elevation was treated as a relative terrain factor in the analysis.

## 7. Weighted Overlay

The four factors were standardised to a common **1–5 suitability scale** and combined using an expert-informed weighted overlay.

| Factor               | Weight |
| -------------------- | -----: |
| Slope                |    30% |
| Distance to drainage |    30% |
| LULC                 |    25% |
| Elevation            |    15% |

The Groundwater Potential Index (GWPI) was calculated as:

**GWPI = (Slope × 0.30) + (Distance to Drainage × 0.30) + (LULC × 0.25) + (Elevation × 0.15)**

The weights were selected for this portfolio assessment and were not statistically calibrated against borehole-yield data.

## 8. GWPI Classification

The final continuous GWPI values ranged from approximately **1.30 to 5.00**.

The index was classified into five relative groundwater potential classes:

* Very Low
* Low
* Moderate
* High
* Very High

The classification is for spatial interpretation and map presentation. It does not represent measured groundwater yield.

## 9. Map Production

Six maps were produced:

1. Study Area
2. Elevation
3. Slope
4. Distance to Drainage
5. Land Use/Land Cover
6. Groundwater Potential

The maps were prepared in QGIS and include the main cartographic elements such as the legend, scale bar, north arrow, CRS and data source.

## 10. Software

* QGIS 3.44.9
* GRASS GIS
* GDAL
