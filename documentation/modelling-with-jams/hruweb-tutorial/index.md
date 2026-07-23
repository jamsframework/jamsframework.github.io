---
layout: doc
title: "HRUweb Tutorial"
section: Tutorials
section_url: /documentation/#modelling-with-jams
---

The HRUweb is a web tool which was developed to delineate hydrological response units (HRU) online. It was implemented in Python and calculates HRUs according to open-source GRASS-GIS algorithms.

After every processing step, the results are provided as raster or shape data which are all compatible with established GIS formats.

For this tutorial, sample data from Rio de Janeiro in Brazil were used.

## Starting HRUweb Tool

**Link to HRU Tool**: [http://intecral.uni-jena.de/hruweb-qs](http://intecral.uni-jena.de/hruweb-qs)

**Structure of HRUweb user interface**

The map window is located in the centre. By using the arrow buttons or the +/- tool bar in the top left, the view can be set manually. The remaining items are located around the map:

1. **Table of Layers**
   1. Change order of layer visibility by using drag and drop
   2. Select a layer by clicking on it. Now the layer can be edited by using the Map Legend.
2. **Map Legend** (→ section Map Legend Description see below)
3. **Wizard**: Processing step description and manual input/settings. Includes the buttons for 'Run' and 'Next'.
4. **Server Log and Results**: Shows the uploading process & provides the result layer as raster or shape file. (→ click on <img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/open_processlog.png' | relative_url }}" alt="open_processlog"> to reveal the item and to hide it again)

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/user_interface.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/user_interface.png' | relative_url }}" alt="user_interface"></a>
    <figcaption>Structure of the HRUweb user interface</figcaption>
  </figure>
</div>

**Map Legend Description**

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/legend_menue.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/legend_menue.png' | relative_url }}" alt="legend_menue"></a>
    <figcaption>Map Legend menu</figcaption>
  </figure>
</div>

1. Remove layer
2. Zoom to map extend: restores smallest possible scale of the map
3. Zoom in the map (<img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/lupe_plus.png' | relative_url }}" alt="lupe_plus">) or zoom out of the map (<img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/lupe_minus.png' | relative_url }}" alt="lupe_minus">)
4. Zoom to previous map extend (backward <img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/pfeil_l.png' | relative_url }}" alt="pfeil_l"> forward)
5. Create bounding box of interest (→ section **Step 2**)
6. Relocate gauge (→ section **Step 6**)
7. User login (→ NEXT STEP)

## Step 0: Check Your Data

**First of all: Do user login!**

Otherwise, your work will not be saved!

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/user_login.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/user_login.png' | relative_url }}" alt="user_login"></a>
    <figcaption>User login</figcaption>
  </figure>
</div>

---

**Check your input data!**

Then, open your input data in a GIS and check them for:

* **completeness**: At least **DEM** and **gauges** are required for delineating HRUs. The rasters of landuse, soil and geology are optional input.
* **projection**: The coordinate system has to be **metric** (like e.g. UTM) in order to enable distance calculations.
* **layer extend**: The layers should have at least the size of the catchment. A base map could be helpful.

| Input data | Description | Format | |
|---|---|---|---|
| DEM | Raster of Digital Elevation Model | Tiff (.tif) or .zip-file | mandatory |
| Gauges | Layer of gauging stations | .zip-file | mandatory |
| Landuse | Raster of landuse | Tiff (.tif) or .zip-file | optional |
| Soil | Raster of soil | Tiff (.tif) or .zip-file | optional |
| Geology | Raster of geology | Tiff (.tif) or .zip-file | optional |

All datasets that are uploaded as ZIP archives need to comply to the following rules:

1. The archive must not contain any subdirectories
2. The archive's name (before .zip) must be identical to the file name(s) inside (e.g., if your Shapefile consists of multiple files named outlets.shp, outlets.dbf, outlets.prj etc., your ZIP archive must be named outlets.zip).

The following sections describe the single substeps in the HRUweb Tool. Each substep is divided into the subsections **Aim**, **Procedure** and **Results**.

## Step 1: Define Data Sources

**Aim**: Upload input data or choose data via catalog.

**Procedure**:

The required input data are described in **Step 0**.

You have two options to define the dem input data:

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/choice_dem.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/choice_dem.png' | relative_url }}" alt="choice_dem"></a>
    <figcaption>Two options to define the DEM input data</figcaption>
  </figure>
</div>

* Upload your own local input data

  or

* Use input data via catalog: choose the DEM you need by clicking on 'add'.
  * **Note**: The chosen DEM is listed in the Table of Layers as a new layer. You can edit it by clicking on the layer and using the Map Legend.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/CATALOG.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/CATALOG.png' | relative_url }}" alt="CATALOG"></a>
    <figcaption>Choosing a DEM from the catalog</figcaption>
  </figure>
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/dem_layer.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/dem_layer.png' | relative_url }}" alt="dem_layer"></a>
    <figcaption>DEM added as a new layer</figcaption>
  </figure>
</div>

The **projection** of the map will be set automatically on the basis of the input data.

For starting the uploading process, click **'Run'** in the Wizard.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/run_next.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/run_next.png' | relative_url }}" alt="run_next"></a>
    <figcaption>'Run' and 'Next' buttons in the Wizard</figcaption>
  </figure>
</div>

**Results**:

The overlays 'Upload' and 'Gauges' are created in the Map View as well as the Table of Layers.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step1.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step1.png' | relative_url }}" alt="overlays_step1"></a>
    <figcaption>'Upload' and 'Gauges' overlays in the Table of Layers</figcaption>
  </figure>
</div>

Zoom into your area of interest. The gauges are shown in light blue dots. The area of the gauges is marked automatically in a red bounding box.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/map_step1.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/map_step1.png' | relative_url }}" alt="map_step1"></a>
    <figcaption>Gauges and automatically created bounding box in the Map View</figcaption>
  </figure>
</div>

**Note**: If the 'Upload' or the 'Gauges' layer are removed, the whole uploading procedure has to be done again by reloading the page.

When finished, click **'Next'**.

## Step 2: Data Setup

**Aim**: Define area of interest for delineating HRUs.

**Procedure**:

In this step, you can specify your region of interest. The red box marks the maximum extend. Data outside of this extend are not delineated.

**Note**: If the red bounding box does already represent your region of interest, you can skip the next step and click **'Run'**.

If you want to specify your region of interest, click on the box symbol <img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/data_setup_use_box.png' | relative_url }}" alt="data_setup_use_box"> in the Map Legend.

By clicking on the symbol, another overlay layer called 'Region' is created.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/region_layer.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/region_layer.png' | relative_url }}" alt="region_layer"></a>
    <figcaption>'Region' overlay layer</figcaption>
  </figure>
</div>

The automatically set red bounding box is now covered by a blue box.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/blue_bbox.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/blue_bbox.png' | relative_url }}" alt="blue_bbox"></a>
    <figcaption>Blue bounding box covering the red default extend</figcaption>
  </figure>
</div>

This blue box represents the area that should be used for delineating HRUs later on. Due to computational reasons, its extend should be fitted to the gauges' positions.

Fit it by clicking on the outline of the blue box and move it at the blue crosses <img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/cross.png' | relative_url }}" alt="cross">.

In order to shift the whole box, drag & drop it by the blue cross in the centre. In order to resize the box, use the cross at the side.

**Note**: The 'Region' layer can be removed without problems. To do so, right-click on the layer and choose "remove". By clicking on <img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/data_setup_use_box.png' | relative_url }}" alt="data_setup_use_box">, the region layer can be restored again.

**Note**: If the extend of the blue box is chosen too small, important parts for delineating HRUs could be left out which makes the results unusable.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/edited_blue_cross.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/edited_blue_cross.png' | relative_url }}" alt="edited_blue_cross"></a>
    <figcaption>Adjusted region box</figcaption>
  </figure>
</div>

For starting the process, click **'Run'**.

**Results**:

A 'Hillshade' overlay is created in the Table of Layers and showed in the Map.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step2.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step2.png' | relative_url }}" alt="overlays_step2"></a>
    <figcaption>'Hillshade' overlay in the Table of Layers</figcaption>
  </figure>
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/result_mapp.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/result_mapp.png' | relative_url }}" alt="result_mapp"></a>
    <figcaption>Hillshade shown in the Map View</figcaption>
  </figure>
</div>

When finished, click **'Next'**.

## Step 3: Data Preparation

**Aim**: Preprocess the DEM by filling its sinks.

If the DEM was already preprocessed that way, no sink filling is necessary.

Otherwise, it is recommended to do so in order to prevent lack of data.

**Procedure**:

Choose "Filling" (default) in the Wizard window, if the sinks should be filled or "No filling", if they should not be filled.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/selection_step3.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/selection_step3.png' | relative_url }}" alt="selection_step3"></a>
    <figcaption>Filling selection in the Wizard</figcaption>
  </figure>
</div>

For starting the process, click **'Run'**.

**Results**:

A DEM with filled sinks is created. Single maps of sinkless elevation, slope and aspect can be downloaded from Server Log.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/databrowser_step3.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/databrowser_step3.png' | relative_url }}" alt="databrowser_step3"></a>
    <figcaption>Downloadable Step 3 results in the Server Log</figcaption>
  </figure>
</div>

**Note**: If filling fails, no maps for slope and aspect are available.

When finished, click **'Next'**.

## Step 4: Reclassification

**Aim**: Reclassify terrain attributes.

**Procedure**:

In this step, the class ranges of slope and aspect can be reclassified and renamed.

In order to change table entries, click in the concerning field and type in the desired value.

"**Old**": lists all existing class ranges

"**New**": assigns IDs to classes

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/class_table_change.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/class_table_change.png' | relative_url }}" alt="class_table_change"></a>
    <figcaption>Reclassification table</figcaption>
  </figure>
</div>

**HELP**

How to choose the best settings for ranges of values of slope and aspect?

For starting the process, click **'Run'**.

**Result**:

The reclassified layers 'aspect' and 'slope' are listed in The Table of Layers.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step4.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step4.png' | relative_url }}" alt="overlays_step4"></a>
    <figcaption>Reclassified 'aspect' and 'slope' layers in the Table of Layers</figcaption>
  </figure>
</div>

Aspect and slope are also shown as maps.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/Aspect.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/Aspect.png' | relative_url }}" alt="Aspect"></a>
    <figcaption>Aspect map</figcaption>
  </figure>
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/Slope.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/Slope.png' | relative_url }}" alt="Slope"></a>
    <figcaption>Slope map</figcaption>
  </figure>
</div>

The reclassified maps of slope and aspect can be downloaded from Server Log as well.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/downloadbrowser_step4.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/downloadbrowser_step4.png' | relative_url }}" alt="downloadbrowser_step4"></a>
    <figcaption>Downloadable Step 4 results in the Server Log</figcaption>
  </figure>
</div>

When finished, click **'Next'**.

## Step 5: Waterflow

**Aim**: Define resolution of the stream network/river system.

**Procedure**:

With each subbasin, one river segment is created. In this step, the maximum number of cells (pixels) for a subbasin of the smallest size has to be specified.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/cellsize.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/cellsize.png' | relative_url }}" alt="cellsize"></a>
    <figcaption>Maximum cell size setting for the smallest subbasin</figcaption>
  </figure>
</div>

In this tutorial, the cellsize was defined by 10.000 pixels.

**HELP**: HOW TO FIND THE BEST MAXIMUM CELL SIZE FOR THE SMALLEST SUBBASIN? / choose the best settings for number of pixels for the smallest subbasin

Depending on, how detailed the river network does look like. Compare to Google Earth.

For starting the process, click **'Run'**.

**Results**:

The layers 'Streams' and 'Subbasins' are created.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step5.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step5.png' | relative_url }}" alt="overlays_step5"></a>
    <figcaption>'Streams' and 'Subbasins' layers in the Table of Layers</figcaption>
  </figure>
</div>

In the map view, the subbasin as well as the stream network layer are shown.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/subbasins.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/subbasins.png' | relative_url }}" alt="subbasins"></a>
    <figcaption>Subbasins map</figcaption>
  </figure>
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/streamnetwork.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/streamnetwork.png' | relative_url }}" alt="streamnetwork"></a>
    <figcaption>Stream network map</figcaption>
  </figure>
</div>

You can download a map of the subbasins in raster and shape format and a vector zip file of stream network from Server Log.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/databrowser_step5.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/databrowser_step5.png' | relative_url }}" alt="databrowser_step5"></a>
    <figcaption>Downloadable Step 5 results in the Server Log</figcaption>
  </figure>
</div>

When finished, click **'Next'**.

## Step 6: Outlets

**Aim**: Check the gauges' position and decide which gauges should be considered.

While creating the subbasins, the gauges' position can differ from the stream network.

**Procedure**:

First of all, use the drag and drop mechanism to change the visibility of the layers in the layer view (→ section **Starting the Webtool**). Order the layer of gauges on top, followed by the layer of streams and the subbasins.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/gauge_top.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/gauge_top.png' | relative_url }}" alt="gauge_top"></a>
    <figcaption>Layer order with gauges on top</figcaption>
  </figure>
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/gauge_top_map.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/gauge_top_map.png' | relative_url }}" alt="gauge_top_map"></a>
    <figcaption>Gauges, streams and subbasins in the Map View</figcaption>
  </figure>
</div>

→ **Check gauges**:

* **Context**: Take a look on the hydrological data - What kind of river properties (amount/velocity of discharge, water level, etc.) were measured? Are the data comprehensible compared to their position in the map?
* **Google Earth**: You can save your shapefile of gauges as a .kml-file and open it in Google Earth. Then zoom in to the gauges. The satellite imagery can be a helpful reference to verify the position of the gauges.

**Note**: The positions can differ significantly in Google Earth, so always doublecheck the positions by its hydrological context!

Now the tool for relocating gauges had to be activated. Click on <img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/relocator.png' | relative_url }}" alt="relocator"> in the legend to activate it. In order to relocate a gauge, click on a gauge and drag it to the proper river segment.

**Note**: For every gauge on a river segment, a catchment is created. If a gauge should not be considered in the further delineation of HRUs, just drag it out of the blue bounding box.

**When you are finished, click on <img class="inline-icon" src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/relocator.png' | relative_url }}" alt="relocator"> to deactivate the tool again!**

For starting the process, click **'Run'**.

**Note**: If you forgot to deactivate the tool, wait until the process is finished and deactivate the tool. Now click on **'Run'** again.

**Results**:

The layer 'Watershed' is listed in the Table of Layers.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step6.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step6.png' | relative_url }}" alt="overlays_step6"></a>
    <figcaption>'Watershed' layer in the Table of Layers</figcaption>
  </figure>
</div>

A map of the watersheds is shown in the Map View and can be downloaded from Server Log.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/MAPview_step6.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/MAPview_step6.png' | relative_url }}" alt="MAPview_step6"></a>
    <figcaption>Watersheds map</figcaption>
  </figure>
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/databrowser_step6.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/databrowser_step6.png' | relative_url }}" alt="databrowser_step6"></a>
    <figcaption>Downloadable Step 6 results in the Server Log</figcaption>
  </figure>
</div>

When finished, click **'Next'**.

## Step 7: Dataoverlay

**Aim**: Computing HRUs.

**Procedure**:

Specify the number of cells (pixels) for the smallest HRU in the wizard. In this tutorial, the number of the smallest HRU was defined by 10.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/nrofcells_step7.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/nrofcells_step7.png' | relative_url }}" alt="nrofcells_step7"></a>
    <figcaption>Number of cells setting for the smallest HRU</figcaption>
  </figure>
</div>

**HELP**: HOW TO FIND THE BEST NUMBER OF CELLS FOR THE SMALLEST HRU?

* HRU should cover between 1-10 ha (10.000 - 100.000 m²) → depends on cell size of the dem used.

For starting the process, click **'Run'**.

**Results**:

The layer 'HRU' is created in the layer overview and shown in the map view.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step7.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/overlays_step7.png' | relative_url }}" alt="overlays_step7"></a>
    <figcaption>'HRU' layer in the Table of Layers</figcaption>
  </figure>
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/mapview7_step7.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/mapview7_step7.png' | relative_url }}" alt="mapview7_step7"></a>
    <figcaption>HRU map</figcaption>
  </figure>
</div>

A map of the created HRUs is provided in the server log.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/download_step7.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/download_step7.png' | relative_url }}" alt="download_step7"></a>
    <figcaption>Downloadable Step 7 results in the Server Log</figcaption>
  </figure>
</div>

When finished, click **'Next'**.

## Step 8: Routing

**Aim**: Creating topology information.

**Procedure**:

In this step, all calculations are done by the WebTool. No user activity is required here.

For starting the process, click **'Run'**.

**Results**:

All routing parameters are available in the server log. They are provided as .csv-tables.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/download_step8.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/download_step8.png' | relative_url }}" alt="download_step8"></a>
    <figcaption>Downloadable Step 8 results in the Server Log</figcaption>
  </figure>
</div>

When finished, click **'Next'**.

## Step 9: Statistics

**Aim**: Collecting statistics per HRU.

**Procedure**:

In this step, all calculations are done by the WebTool. No user activity is required here.

For starting the process, click **'Run'**.

In order to see the results, click **'Next'**.

**Results**:

Shapefiles of the HRUs as well as their parameters can be downloaded from the server log.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/download_step9.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/download_step9.png' | relative_url }}" alt="download_step9"></a>
    <figcaption>Downloadable Step 9 results in the Server Log</figcaption>
  </figure>
</div>

The results of all steps can be downloaded in a zip-file.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/zip_step9.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/zip_step9.png' | relative_url }}" alt="zip_step9"></a>
    <figcaption>Download all results as a zip-file</figcaption>
  </figure>
</div>

---

**FINISHED**

If the delineation shall be repeated, click on:

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/new_step9.png' | relative_url }}"><img src="{{ '/assets/img/documentation/modelling-with-jams/hruweb-tutorial/new_step9.png' | relative_url }}" alt="new_step9"></a>
    <figcaption>Restart the delineation</figcaption>
  </figure>
</div>
