---
layout: doc
title: "J2K: Transform Daily into Hourly Model"
section: Modelling with JAMS
section_url: /documentation/#modelling-with-jams
---

## Overview

To convert a standard daily J2K hydrological model to hourly resolution, implement these modifications:

## Required Changes

1. **Time Series Input**

   Convert all time series data to hourly time steps

2. **Model Time Step**

   Modify the general time step setting in the main J2K context

3. **Component Parameters**

   Search for `tempRes` across all components and change from daily (d) to hourly (h)

4. **Time-Dependent Parameters**

   *Soil Module (J2KProcessLumpedSoilWater):*
   - Maximum percolation speed (e.g., 20mm/d &rarr; 0.83mm/h)
   - Maximum infiltration rate for summer/winter (mm/d &rarr; mm/h)
   - Test results carefully for overland flow and interflow generation

   *Groundwater Module (J2KProcessGroundwater):*
   - RG1/RG2 outflow coefficient (10d &rarr; 240h)

5. **Precipitation Elevation Correction**

   Set `elevationCorrection` parameter to "false" in HRULoop/regionalization/precipRegionalization module

6. **Unit Conversion**

   Change from L/d to L/h in the unit conversion module

7. **Efficiency Calculator**

   Modify unit parameter from daily (d) to hourly (h)
