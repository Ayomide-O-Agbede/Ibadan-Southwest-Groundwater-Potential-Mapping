# Processing Notes

## Purpose

This document records important processing decisions, failed approaches, corrections and methodological changes made during the groundwater potential assessment of Ibadan Southwest LGA.

Documenting these steps provides transparency and preserves the actual development of the workflow.

## 1. Coordinate Reference System

The main analysis was standardized to:

**WGS 84 / UTM Zone 31N (EPSG:32631)**

A projected CRS was used because several processing steps involved distances and terrain calculations that are more appropriate in a coordinate system measured in metres.

## 2. Slope Calculation Correction

The first slope calculation was identified as unsuitable because the DEM was being processed in a geographic coordinate system.

The DEM was subsequently reprojected to EPSG:32631 and the slope was recalculated.

The corrected slope raster produced values ranging from approximately 0° to 16.22°.

**Lesson:** Terrain derivatives should be generated using an appropriate projected CRS when accurate distance-based calculations are required.

## 3. DEM Sink Filling

A filled DEM was generated using the QGIS Fill Sinks (Wang & Liu) algorithm.

The filled DEM was used for subsequent hydrological processing, particularly flow accumulation and stream-network extraction.

## 4. Initial Flow Accumulation

The first flow-accumulation output contained negative values.

Because negative accumulation values were unsuitable for the intended stream-extraction workflow, this output was rejected.

A new flow-accumulation raster was generated using the GRASS `r.watershed` tool with the positive flow-accumulation option.

The corrected output was subsequently used for stream-network extraction.

## 5. Stream Network Extraction

A drainage/stream network was extracted from the positive flow-accumulation raster using a threshold of 1000.

The resulting binary stream network showed a continuous branching drainage pattern across the study area.

Attempts were made to thin and vectorize the stream network. These attempts did not produce a satisfactory result and were therefore not used in the final workflow.

The raster stream network was retained for calculating distance to drainage.

## 6. Distance to Drainage Correction

Distance to drainage was initially calculated from the stream network.

The first suitability classification was based on the full raster extent rather than only the study-area extent. This caused the classification range to be strongly influenced by values outside the study boundary and resulted in poor visual separation within the study area.

The actual distance raster was therefore clipped to the study boundary.

The clipped raster had a maximum distance of approximately 1623.62 m within the study area.

The suitability classification was recalculated using the range of the clipped raster.

This corrected distance-to-drainage suitability raster was used in the final groundwater potential index.

## 7. CHIRPS Rainfall Processing

CHIRPS annual rainfall data for 2001–2025 were investigated as a possible groundwater-related factor.

An initial attempt was made to reproject individual annual CHIRPS rasters to EPSG:32631 using bilinear resampling.

This produced NoData-related edge artefacts, including values close to -9997, making the resulting rasters unsuitable for reliable analysis.

Several cleaning and NoData-handling attempts were tested but did not provide a satisfactory workflow.

A more reliable approach was then adopted:

i. The original annual CHIRPS rasters were retained in their original geographic coordinate system.
ii. A mean annual rainfall raster for 2001–2025 was calculated using the original rasters.
iii. NoData values were ignored during the calculation.
iv. The resulting mean rainfall raster was then reprojected to EPSG:32631.

Although this produced a valid long-term mean rainfall surface, CHIRPS has a relatively coarse spatial resolution compared with the ~30 m terrain analysis used for the study.

Rainfall was therefore excluded from the final weighted overlay rather than introducing a coarse-resolution factor into a detailed local assessment.

## 8. LULC Processing

ESA WorldCover 2021 v2.0 was selected as the land-use/land-cover dataset.

The original 10 m WorldCover raster was reprojected to EPSG:32631 using nearest-neighbour resampling and clipped to the study boundary.

The resulting land-cover classes were reclassified into groundwater suitability scores from 1 to 5.

Because the other major analytical factors were based on approximately 30 m terrain data, the LULC suitability raster was resampled to match the approximately 30 m analysis grid using nearest-neighbour resampling.

## 9. Suitability Reclassification

The selected factors were standardized to a common suitability scale:

**1 = Very Low**

**2 = Low**

**3 = Moderate**

**4 = High**

**5 = Very High**

The following factors were standardized:

- Slope
- Distance to drainage
- LULC
- Elevation

This allowed the factors to be combined using a weighted overlay.

## 10. Initial Groundwater Potential Index

An initial groundwater potential index was calculated using:

- Slope — 30%
- Distance to drainage — 30%
- LULC — 25%
- Elevation — 15%

The initial GWPI was later superseded after the distance-to-drainage raster was corrected by clipping it to the study boundary and recalculating its suitability classification.

## 11. Final Groundwater Potential Index

The corrected groundwater potential index was calculated using the corrected distance-to-drainage suitability layer.

The final model was:

`GWPI = (Slope × 0.30) + (Distance to Drainage × 0.30) + (LULC × 0.25) + (Elevation × 0.15)`

The final raster is:

`Ibadan_Southwest_Groundwater_Potential_Index_v2`

The final GWPI has values ranging approximately from 1.30 to 5.00.

## 12. Interpretation

The final map represents **relative groundwater potential** based on the selected GIS factors.

It should not be interpreted as a direct prediction of groundwater yield.

The weighting scheme was expert-informed for this portfolio assessment and was not statistically calibrated because spatial borehole validation data were not available.

The result is therefore intended primarily for groundwater exploration planning and spatial prioritization.

## 13. Key Processing Lessons

Several practical lessons emerged during the project:

- Use an appropriate projected CRS before calculating terrain and distance-based derivatives.
- Inspect raster statistics instead of relying only on visual appearance.
- Check the spatial extent of derived rasters before classification.
- Handle NoData values carefully when working with satellite and rainfall datasets.
- Match raster grids before performing weighted overlay calculations.
- Preserve failed processing attempts during project development so that methodological decisions can be traced.
- Distinguish between a relative GIS-based potential index and validated groundwater productivity.