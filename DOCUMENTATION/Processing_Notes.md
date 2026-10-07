# Processing Notes

This document records the main processing decisions, corrections and approaches that were changed during the project.

## 1. Coordinate Reference System

The analysis was standardised to **WGS 84 / UTM Zone 31N (EPSG:32631)**.

The projected CRS was necessary because slope, distance and other spatial calculations were being carried out in metres.

## 2. Slope Correction

The first slope output was generated before the DEM was properly standardised to the projected CRS.

This was corrected by reprojecting the DEM to EPSG:32631 and deriving slope again. The corrected slope range was approximately **0–16.22°**.

## 3. DEM Sink Filling

A filled DEM was generated using the **Wang & Liu** sink-filling method in QGIS.

This was done before the flow-accumulation and drainage analysis to improve the hydrological processing.

## 4. Flow Accumulation

The first flow-accumulation output contained negative values, so it was not used.

The flow accumulation was regenerated using **GRASS GIS `r.watershed`**, and the corrected positive output was used for drainage extraction.

A threshold of **1000** was selected for the drainage network.

## 5. Drainage Network and Distance

Different attempts were made to thin or vectorise the extracted drainage network, but the results were not satisfactory for the distance analysis.

The raster drainage network was therefore retained and used to calculate distance with **GDAL Proximity**.

## 6. Distance-to-Drainage Correction

The first distance suitability classification was affected by values outside the actual study area.

The distance raster was therefore clipped to the LGA boundary before calculating the final suitability classes.

The corrected maximum distance was approximately **1623.62 m**, and the revised suitability classes were used in the final GWPI.

## 7. CHIRPS Processing

CHIRPS annual rainfall data from **2001–2025** were initially investigated as an additional groundwater-related factor.

Reprojecting individual rainfall rasters to EPSG:32631 using bilinear resampling produced NoData edge effects around the original **-9997** values. Several cleaning attempts did not give a satisfactory result.

The rainfall data were instead processed in their original CRS while handling the NoData values, and the resulting mean annual rainfall surface was then reprojected.

The rainfall surface was usable, but its approximately **0.05° resolution** was considered too coarse for the final analysis. It was therefore excluded from the weighted overlay.

## 8. LULC Processing

ESA WorldCover 2021 v2.0 was used for the LULC factor.

The 10 m raster was reprojected using nearest-neighbour resampling, clipped to the study area and reclassified to a 1–5 suitability scale.

It was then resampled to approximately the 30 m analysis grid using nearest neighbour.

## 9. Final GWPI

An initial GWPI was produced before the distance-to-drainage correction.

After correcting the distance raster and its suitability classes, the GWPI was recalculated.

The final raster is:

`Ibadan_Southwest_Groundwater_Potential_Index_v2.tif`

The final GWPI range was approximately **1.30–5.00**.

## 10. Interpretation

The final result represents **relative groundwater potential**, not measured groundwater yield.

The weights were expert-informed and the model was not validated against spatial borehole-yield data. The result is therefore intended for **initial groundwater exploration and spatial planning**.

## 11. Main Lessons

* Use a projected CRS for distance and terrain analysis where calculations are required in metres.
* Check raster statistics before using derived outputs.
* Check the analysis extent and NoData areas before classification.
* Keep the raster grids consistent when combining factors.
* Record failed processing steps and corrections.
* Distinguish a relative groundwater potential index from a validated groundwater productivity assessment.
