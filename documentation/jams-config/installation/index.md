---
layout: doc
title: JAMS Installation
section: JAMS Setup & Configuration
section_url: /documentation/#jams-setup
---

## Release Versions

JAMS is distributed as a platform-independent archive — there is no installer. Download the [latest release](https://github.com/jamsframework/jams/releases/latest) and unpack it at a location of your choice, or build it yourself from source (see [Downloads]({{ '/downloads/' | relative_url }})). For information about the contents, please have a look at the [JAMS Download Package]({{ '/documentation/jams-config/jams-download-package/' | relative_url }}) page.

## System Requirements

Running JAMS requires a **Java Runtime, version 17 or newer**. On macOS, use Java 24 or newer if you hit a rare accessibility-related crash (a JDK bug fixed in Java 24). Building JAMS from source additionally requires a JDK 17+ (Maven and all third-party dependencies are included via the Maven wrapper).

## Directory Layout and Location

After unpacking JAMS (or after building it from source — the build output lands in `jams-bin`) you will find a folder with the following content:

- **components:** folder containing component libraries (*.jar)
- **data**: folder containing demo models with test datasets
- **lib**: folder containing all libraries required to run JAMS and its modelling components
- **jams.sh, jams.bat**: scripts for running the JAMS Launcher
- **juice.sh, juice.bat**: scripts for running the JAMS Builder

The JAMS installation directory can easily be moved to other locations on the same or other computers — apart from a suited Java version there exist no external dependencies for running JAMS. If you want to build your own JAMS components, see [Setting up a JAMS Development Environment]({{ '/documentation/jams-config/setting-up-a-jams-development-environment/' | relative_url }}).
