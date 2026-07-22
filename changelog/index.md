---
layout: page
title: Changelog
description: "Version history and release notes for JAMS."
---

Historical release notes for past JAMS versions, newest first. Going forward, release notes for new versions are published directly on the [GitHub Releases](https://github.com/jamsframework/jams/releases) page.

<details class="pub-accordion" open>
  <summary>Version 3.17 <span class="pub-count">(2025-11-26)</span></summary>
  <div class="changelog-body">
<h4><strong>Software Improvements and Bug Fixes</strong></h4>
<ul>
<li>minor usability improvements to the JAMS GUI / window layout</li>
</ul>
<h4><strong>New / Improved Model Components</strong></h4>
<ul>
<li><strong>J2K_iso</strong>
<ul>
<li>model components for the simulation of isotope mixing, unmixing and transport</li>
</ul>
</li>
<li><strong>jams.components.io.TSDataStoreReader</strong>
<ul>
<li>adapted to work with different calendar types as found in some climate models (standard calendar, 360-day calendar, standard calendar w/o leap years)</li>
</ul>
</li>
</ul>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.16 <span class="pub-count">(2024-12-02)</span></summary>
  <div class="changelog-body">
<h4><strong>Software Improvements and Bug Fixes</strong></h4>
<ul>
<li>minor usability improvements to the JAMS GUI / window layout</li>
</ul>
<h4><strong>New / Improved Model Components</strong></h4>
<ul>
<li><strong>jams.components.core.TemporalFileInputContext</strong>
<ul>
<li>complete rework of the component</li>
<li>component allows to iterate over time steps defined in a JAMS timeseries input file</li>
</ul>
</li>
<li><strong>jams.components.io.TSDataStoreReader</strong>
<ul>
<li>adapted to work with new TemporalFileInputContext</li>
</ul>
</li>
<li><strong>jams.components.io.unidata.EntityCollectionFromList (new)<br></strong>
<ul>
<li>extract an entity collection object from a NetCDF file</li>
</ul>
</li>
<li><strong>jams.components.io.unidata.NetCDFReader3D</strong>
<ul>
<li>various improvements</li>
</ul>
</li>
<li><strong>optas.efficiencies.UniversalEfficiencyCalculator</strong>
<ul>
<li>added KGE to the efficiencies calculated by the UniversalEfficiencyCalculator, as well as a weighted version, and a version returning its 3 components r, gamma, beta</li>
</ul>
</li>
<li><strong>jams.components.calc.DoubleArrayDivide (new)<br></strong>
<ul>
<li>added component for dividing all elements of a DoubleArray</li>
</ul>
</li>
<li><strong>jams.components.indices.ClimateIndicesForest</strong>
<ul>
<li>added some outputs</li>
</ul>
</li>
<li><strong>jams.components.io.DataSerializer (new)<br></strong>
<ul>
<li>combines observed and simulated values for different locations into one large list of obervations and simulations</li>
</ul>
</li>
<li><strong>jams.components.datatransfer.DoubleTransfer<br></strong>
<ul>
<li>Added option to copy/overwrite value</li>
</ul>
</li>
<li><strong>jams.components.data.EntityDoubleAccess (new)<br></strong>
<ul>
<li>Added component to get double values by name from an entity and store it</li>
</ul>
</li>
</ul>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.15 <span class="pub-count">(2023-02-05)</span></summary>
  <div class="changelog-body">
<h4><strong>Software Improvements and Bug Fixes</strong></h4>
<ul>
<li>improvement to the JAMS GUI / window layout</li>
<li>usability improvements to the Data Explorer</li>
<li>added option to define standard output data directory via properties file</li>
</ul>
<h4><strong>New / Improved Model Components</strong></h4>
<ul>
<li><strong>jams.components.io.unidata.NetCDFReader</strong>, <strong>jams.components.io.unidata.TimeIntervalFromNetCDF</strong>
<ul>
<li>read spatio-temporal data from from a NetCDF file</li>
<li>creates a time interval attribute from a NetCDF file, e.g. for iterating over all of its time steps</li>
</ul>
</li>
<li><strong>jams.components.io.TimeIntervalFromDataStore</strong>
<ul>
<li>creates a time interval attribute from a datastore, e.g. for iterating over all time steps in an input dataset</li>
</ul>
</li>
<li><strong>jams.components.aggregate.MinMax</strong>
<ul>
<li>calculates min/max of incoming values</li>
</ul>
</li>
<li><strong>jams.components.aggregate.SpatioTemporalAggregator</strong>
<ul>
<li>improved aggregation options for spatio-temporal data</li>
</ul>
</li>
<li><strong>jams.components.statistics.PercentileCalc</strong>
<ul>
<li>caculates percentile values from input data</li>
</ul>
</li>
<li><strong>jams.components.io.TemporalShapeEntityWriter</strong>
<ul>
<li>improved handling of temporary files</li>
</ul>
</li>
<li><strong>jams.components.io.TemporalShapeEntityWriter</strong>
<ul>
<li>added function to auto-create subdirectories based on name</li>
</ul>
</li>
</ul>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.14 <span class="pub-count">(2021-11-06)</span></summary>
  <div class="changelog-body">
<h4><strong>New Model Components</strong></h4>
<ul>
<li>org.unijena.j2k.inputData.RecalcLanduseStateVars
<ul>
<li>recalculation of landuse state variables during simulation, e.g. for landuse changes</li>
</ul>
</li>
<li>org.unijena.j2k.topology.ReachSubbasin, org.unijena.j2k.topology.SubbasinArea, org.unijena.j2k.io.SubbasinLink
<ul>
<li>extraction of all HRUs belonging to a reach subbasin as a list</li>
<li>calculation of the area of a reach subbasin</li>
</ul>
</li>
<li>jams.components.indices.SnowLine
<ul>
<li>calculation of snow line elevation</li>
</ul>
</li>
</ul>
<h4><strong>Improvements and Bug Fixes</strong></h4>
<ul>
<li>minor bug fixes and improvement to the JAMS runtime system and GUI</li>
</ul>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.13 <span class="pub-count">(2020-04-22)</span></summary>
  <div class="changelog-body">
<h4><strong>New Example Model</strong></h4>
<p>A new J2K hydrological model for the Dudh Koshi River Basin with all required data and additional components for glacier processes simulation is available in the data folder. Thanks to <a href="https://www.icimod.org/team/santosh-nepal">Santosh Nepal</a> from ICIMOD/Kathmandu for providing this dataset!</p>
<h4><strong>New Model Components<br />
</strong></h4>
<ul>
<li>org.unijena.j2k.regionalisation.Regionalisation_IDW is a component that implements interpolation based on Inverse Distance Weighting (IDW) with the following improvements:
<ul>
<li>Intergrating all required functionality in one component without an additional initialization component, it allows to streamline and simplify model structure.</li>
<li>In addition to data interpolation, it allows to calculate and output information about average station distance and station elevation difference at each time step, provoding improved insight into the spatial and temporal distribution of station information density.</li>
</ul>
</li>
<li>jams.components.data.DateComponents allows to extract single components from a date object</li>
<li>jams.components.data.ScalarToArray allows to collect double scalar(s) into double array(s)</li>
<li>jams.components.indices.SPICalc, jams.components.indices.DataColllector and jams.components.indices.DateCollector are components for calculation of Standardized Precipitation Index (SPI) and for collecting respective precip and calendar values</li>
<li>jams.components.calc.DoubleArrayMultiply allow to multiply elements in a double array with one or many double values</li>
<li>jams.components.data.CalendarComponentChanged allows to detect changes in a component of a date object and thus to perform actions at certain time periods (e.g. monthly, yearly in a daily model)</li>
</ul>
<h4><strong>Improvements and Bug Fixes</strong></h4>
<ul>
<li>added support for Datastore outputs of TemporalNestedContext</li>
<li>minor bug fixes and improvement to the JAMS runtime system and GUI</li>
</ul>
<h1>Revision 01</h1>
<ul>
<li>minor fixes in the Dudh Koshi example model</li>
</ul>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.12 <span class="pub-count">(2019-10-11)</span></summary>
  <div class="changelog-body">
<h4><strong>New J2K Components<br />
</strong></h4>
<ul>
<li>org.unijena.j2k.regionalisation.LapseRateRegionalization is a lapse rate component, taking into account distance to stations, missing data and yearly or monthly lapse rates</li>
<li>org.unijena.j2k.regionalisation.LapseRateAdaptation can be used in combination with the IDW regionalization to apply a lapse rate approach in the interpolated climatic variable. For this purose, IDW can now output the average (weighted) elevation of the source stations. This elevation can then be used in LapseRateAdaptation to adapt the IDW result according to the elevation difference between the HRU and the source station elevations</li>
</ul>
<h5>Revision 01:</h5>
<ul>
<li>added lower/upper  boundary options to org.unijena.j2k.regionalisation.LapseRateRegionalization and org.unijena.j2k.regionalisation.LapseRateAdaptation</li>
</ul>
<h5>Revision 02:</h5>
<ul>
<li>fixed bug in org.unijena.j2k.regionalisation.LapseRateRegionalization and org.unijena.j2k.regionalisation.LapseRateAdaptation</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.11_00 <span class="pub-count">(2019-07-10)</span></summary>
  <div class="changelog-body">
<h4><strong>Improvements to JAMS<br />
</strong></h4>
<ul>
<li>added dependencies to run under Java 9 and above</li>
</ul>
<h4><strong>New JAMS Components<br />
</strong></h4>
<ul>
<li>added support for <em>R</em> integration</li>
<li>added components for calculation of indicators (package <em>jams.components.indices</em>), e.g.
<ul>
<li>Indicators of Hydrological Alteration (IHA)</li>
<li>Various precipitation indicators including Standardized Precipitation Index (SPI)</li>
</ul>
</li>
</ul>
<p> </p>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.9_03 <span class="pub-count">(2018-07-14)</span></summary>
  <div class="changelog-body">
<h4><strong>Improvements to JAMS Components<br />
</strong></h4>
<ul>
<li>added/fixed components for simple artithmetics in jams.components.calc: DoubleAdd, DoubleSubstract, DoubleMultiply, DoubleDivide</li>
</ul>
<h4><strong>Improvements to JAMS Worldwind<br />
</strong></h4>
<ul>
<li>fixed a bug in Worldwind classifier</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.9_00/01/02 <span class="pub-count">(2018-06-11)</span></summary>
  <div class="changelog-body">
<h4><strong>Improvements to JAMS Components<br />
</strong></h4>
<ul>
<li>added new component jams.components.aggregate.LongTermAggregation for calculating long-term sums or averages</li>
<li>added new component jams.components.gui.CategoryPlot that creates a graphical plot of category data, e.g. to compare attributes of different model entities</li>
<li>added various components for SMDI/ETDI calculation (https://doi.org/10.1016/j.agrformet.2005.07.012)</li>
<li>added component jams.components.calc.EventCounter that allows counting the occurrence of certain states in a model (e.g. SMDI < -3.5)</li>
<li>fixed minor bug in jams.components.gui.CategoryPlot</li>
</ul>
<h4><strong>Updated J2K example model<br />
</strong></h4>
<ul>
<li>added components for long-term temporal aggregation and output</li>
<li>added components for Shapefile output of results</li>
<li>replaced efficiency calculation component by more versatile version</li>
<li>added category plots for efficiencies and water balance</li>
</ul>
<h4><strong>Improvements to JAMS Optas</strong></h4>
<ul>
<li>addeed optas.sampler.FileListSampler that allows sampling over a list of given parameter values read from a file</li>
<li>fixed minor bug in Efficiency Configurator</li>
</ul>
<h4><strong>Improvements to JAMS Main<br />
</strong></h4>
<ul>
<li>added option to use minutely time steps</li>
</ul>
<p> </p>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.8_00 <span class="pub-count">(2017-06-24)</span></summary>
  <div class="changelog-body">
<h4><strong>Improvements to JAMS OPTAS<br />
</strong></h4>
<p>fixed functionality for assisted configuration of model efficiency calculation. For a detailed description, have a look at the new <a href="/documentation/jams-features/efficiency_calculation/">Efficiency Calculation article</a>.</p>
<img src="{{ '/assets/img/changelog/img_5940582f52d35.png' | relative_url }}" alt="Efficiency configuration dialog" style="max-width: 441px;">
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.7_00 <span class="pub-count">(2017-05-05)</span></summary>
  <div class="changelog-body">
<h4><strong>New and updated components</strong></h4>
<p>added components to calculate <em>Soil Moisture Deficit Index</em> (SMDI) and <em>Evapotranspiration Deficit Index</em> (ETDI) (see jams.components.indices in jams-components library)</p>
<p>added function to output the impact of indivudual stations within the <em>Inverse Distance Weighting</em> (IDW) regionalization approach, e.g. as XY-plot or as map</p>
<div class="img-gallery">
  <img src="{{ '/assets/img/changelog/JAMS-WorldWind_station_impact.png' | relative_url }}" alt="JAMS WorldWind station impact" style="max-width: 290px;">
  <img src="{{ '/assets/img/changelog/station_weights.png' | relative_url }}" alt="Station weights" style="max-width: 290px;">
</div>
<h4><strong>Minor bug fixes</strong></h4>
<ul>
<li>fixed GUI errrors in WorldWind</li>
<li>fixed GUI error in Data Explorer (JADE)</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.6_00 <span class="pub-count">(2017-03-27)</span></summary>
  <div class="changelog-body">
<p>Improvements in the WorldWind data viewer:</p>
<ul>
<li>auto-play function to visualize time-series with given time delay</li>
</ul>
<img src="{{ '/assets/img/changelog/2017-03-27-11_07_41-JAMS-WorldWind.png' | relative_url }}" alt="JAMS WorldWind" style="max-width: 391px;">
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.5_00 <span class="pub-count">(2017-03-06)</span></summary>
  <div class="changelog-body">
<p>Improvements in the JAMS data I/O &amp; Data Explorer (JADE):</p>
<ul>
<li>functions to define decimal places in table views (see JAMS preferences)</li>
<li>J2K input datastores can use english date/time formats</li>
</ul>
<p>Improvements in the JAMS Cloud client:</p>
<ul>
<li>display of job progress</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.4_00 <span class="pub-count">(2016-11-14)</span></summary>
  <div class="changelog-body">
<p>Improvements in the JAMS Model Builder (JUICE):</p>
<ul>
<li>functions for remote simulation including
<ul>
<li>running models on remote servers</li>
<li>browsing remote workspaces/jobs</li>
<li>synchronizing remote and local workspaces</li>
</ul>
</li>
</ul>
<p>Improvements in the JAMS Data Explorer (JADE):</p>
<ul>
<li>functions for easily transferring parameter optimization results to models</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.2_00 <span class="pub-count">(2016-08-19)</span></summary>
  <div class="changelog-body">
<p>Improvements in the JAMS Model Builder (JUICE):</p>
<ul>
<li>display of component attribute default values, units and descriptions</li>
</ul>
<p>Added components to the jams-components repository:</p>
<ul>
<li>component for performing Empirical Mode Decomposition (EMD) on time series data (jams.components.analysis.EMD)</li>
<li>component that applies Local Kriging for spatial data interpolation using JGrassGears library (jams.components.interpolation.RegionalisationLocalKriging)</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.1_00 <span class="pub-count">(2016-06-03)</span></summary>
  <div class="changelog-body">
<p>This version brings some new features for the JAMS Data Explorer (JADE):</p>
<ul>
<li>new filter function for time step selection</li>
<li>improved aggregator options</li>
<li>area weighting also for cross-product calculation</li>
<li>better copy/paste support for spreadsheet data</li>
</ul>
<p>For the WorldWind viewer, the following functions were added:</p>
<ul>
<li>area weighting / unit conversion for data to be visualized</li>
<li>improved opacity control for polygon outlines (including complete removal of outlines)</li>
<li>detailed information for individual entities with time-series plotting function</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.0_03 <span class="pub-count">(2016-05-17)</span></summary>
  <div class="changelog-body">
<p>Minor updates:</p>
<ul>
<li>updated WorldWind libraries for better performance</li>
<li>fixed minor bug in aggregation functions for spatio-temporal output datastores</li>
<li>fixed bug in TemporalSumAggregator (month filters)</li>
<li>Added MODIS ET reader components that allow to use MODIS global terrestrial evapotranspiration data for hydrological modelling</li>
<li>updated Netbeans projects, build scripts and starter scripts</li>
<li>improved installer with Java version check</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.0_02 <span class="pub-count">(2016-02-10)</span></summary>
  <div class="changelog-body">
<h4>Minor bug fix</h4>
<ul>
<li>fixed incompatibility problem with older output datastores</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.0_01 <span class="pub-count">(2016-02-08)</span></summary>
  <div class="changelog-body">
<h4>Minor changes in component package structure</h4>
<ul>
<li>moved core components Context, TemporalContext and SpatialContext to jams-components.jar library (package jams.components.core)</li>
<li>added function to automatically adapt existing models to reflect these changes</li>
<li>fixed minor issues in documentation generator</li>
<li>minor improvements in JAMS Builder GUI</li>
</ul>
<div style="clear:both;"></div>
  </div>
</details>

<details class="pub-accordion">
  <summary>Version 3.0b26 <span class="pub-count">(2015-11-13)</span></summary>
  <div class="changelog-body">
<h4>JAMS file association</h4>
<p>When using the automatic Windows installer, JAMS model files (*.jam) are automatically associated to the JAMS Launcher, allowing to quickly load a model by double-clicking the file.</p>
<h4>Separation of JAMS platform libraries and component libraries</h4>
<p>JAMS platform libraries are now strictly separated from component libraries. This is reflected by a new sub-directory named <strong><em>components</em> </strong>within your JAMS installation which by default includes all your component libraries. Of course, it is still possible to include component libraries from every directory on your computer by defining individual library locations in your JAMS settings.</p>
<div style="clear:both;"></div>
  </div>
</details>
