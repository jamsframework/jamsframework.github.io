---
layout: doc
title: JAMS Download Package
section: JAMS Setup & Configuration
section_url: /documentation/#jams-setup
---

## Versions

JAMS is offered in two distributions:

1. A **Windows installer** for straightforward setup on Windows
2. A **platform-independent zip-archive** for Java-compatible systems

Installation guidance is available in the [JAMS Installation]({{ '/documentation/jams-config/installation/' | relative_url }}) documentation.

## Features

Both versions include identical capabilities:

- **JAMS runtime system** containing core operational components
- **Modelling libraries** with 200+ components for:
  - Simulating hydrological and environmental phenomena
  - Data analysis, input/output, and visualization functions
- **Graphical user interfaces** for:
  - Model development, configuration, and execution (*JAMS Launcher* and *JAMS Builder*)
  - Data exploration and visualization (*JAMS Data Explorer*) with 3D mapping via [NASA World Wind](http://worldwind.arc.nasa.gov)
- **OPTAS toolbox** for model calibration through parameter optimization, sensitivity, and uncertainty analysis
- Automated **documentation generator** using DocBook, XSLT, and Apache FOP (Windows only)

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/jams-config/jams-download-package/JUICE.png' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-config/jams-download-package/JUICE.png' | relative_url }}" alt="JUICE"></a>
    <figcaption>JAMS Builder</figcaption>
  </figure>
  <figure>
    <img src="{{ '/assets/img/documentation/jams-config/jams-download-package/JAMSWorldWind-300x255.png' | relative_url }}" alt="JAMSWorldWind">
    <figcaption>Result visualization using NASA World Wind</figcaption>
  </figure>
  <figure>
    <a href="{{ '/assets/img/documentation/jams-config/jams-download-package/JAMSplot2.png' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-config/jams-download-package/JAMSplot2.png' | relative_url }}" alt="JAMSplot2"></a>
    <figcaption>JAMS runtime plot</figcaption>
  </figure>
</div>

## Demo Models

Two demonstration models showcase JAMS functionality:

1. USGS **Thornthwaite** model — a simplified monthly water-balance simulation [1]
2. **J2K** — a fully distributed hydrological process model [2]

Models reside in the installation's "data" subdirectory. To execute:

1. Launch JAMS Builder; select "File" → "Load Model..."
2. Navigate to "data/j2k_gehlberg" or "data/thornthwaite" folder
3. Open "j2k_gehlberg.jam" or "thornthwaite.jam"
4. Select "Model" → "Run Model" (or the <img class="inline-icon" src="{{ '/assets/img/documentation/jams-config/jams-download-package/ModelRun.png' | relative_url }}" alt="ModelRun"> toolbar button) to begin simulation

## References

[1] McCabe, G. J. & Markstrom, S. L. (2007). A Monthly Water-Balance Model Driven By a Graphical User Interface (Open-File Report No. 2007–1088). U.S. Geological Survey.

[2] Krause, P. (2002). Quantifying the impact of land use changes on the water balance of large catchments using the J2000 model. *Physics and Chemistry of the Earth, Parts A/B/C* **27**(9–10), 663–673. doi:10.1016/S1474-7065(02)00051-7
