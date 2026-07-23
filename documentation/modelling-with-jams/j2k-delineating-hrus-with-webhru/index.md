---
layout: doc
title: "J2K: Delineating HRUs with WebHRU"
section: Tutorials
section_url: /documentation/#modelling-with-jams
---

## Overview

webHRU represents an updated version of the previous HRUweb tool. The interface and processing routines have been completely reimplemented, though the fundamental delineation workflow remains consistent.

**Access:** [http://riker.geogr.uni-jena.de/webhru](http://riker.geogr.uni-jena.de/webhru)

## Key Requirements

### Dataset Specifications

All input datasets must utilize identical UTM projection parameters. Gauging station data requires specific formatting as a zipped Shapefile with these characteristics:

- The Shapefile name matches the ZIP file name exactly
- No directory structures exist within the ZIP; only Shapefile component files
- An integer attribute named "id" (case-sensitive) is mandatory
- The "id" field contains unique station identifiers greater than zero

### User Interface Considerations

During steps 1 and 4, map-based user inputs require manual transfer to input fields using *Subregion from Map* or *Positions from Map* buttons prior to executing the *RUN* command.

Browser window width may affect button responsiveness. The recommended solution involves fullscreen mode or adjusting zoom settings to ensure proper functionality.

### Station Positioning Workflow

Step 4 demands precise positioning of stations on the stream network:

- Zoom closely to individual gauges
- Click to enable each point (white border indicates active state)
- Drag points to desired river segment locations
- Reposition slightly if subcatchments fail to generate
- Move unwanted stations beyond the main basin boundary
- Press *Positions from Map* after completion

### Output Files

Downloaded results require manual filename modification for JAMS compatibility.
