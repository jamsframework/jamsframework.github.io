---
layout: doc
title: JAMS Installation
section: JAMS Setup & Configuration
section_url: /documentation/#jams-setup
---

## Release Versions

The JAMS binary release comes in two flavors:

1. as a Windows installer and
2. as a platform-independent zip-archive.

After starting it, the Windows installer will ask for an installation directory, copy all required files to that location and create shortcuts on the Desktop and in the Start Menu. In the case of the zip-archive, the user just unpacks the archive at a location of choice. For information about the contents, please have a look at the [JAMS Download Package]({{ '/documentation/jams-config/jams-download-package/' | relative_url }}) page.

## System Requirements

For running JAMS, a **Java Runtime Environment (JRE) version 1.7 or higher** is required. When using the Windows installer, it will automatically check for a suited Java environment and offer to download one if it is not existing yet. If using the platform-independent archive, the user must ensure that a suited Java **version** is installed and that the **architectures** of Java and operating system do match (both 32bit or both 64bit).

## Directory Layout and Location

After installing / unpacking JAMS you will find a folder with the following content:

- **components:** folder containing component libraries (*.jar)
- **data**: folder containing two test models with test datasets
- **dev**: folder with preconfigured Netbeans IDE projects for building own JAMS components
- **lib**: folder containing all libraries required to run JAMS and its modelling components
- **jams.bat, juice.bat**: Windows batch files for running the JAMS Launcher and the JAMS Builder respectively
- **jams.sh, juice.sh**: Shell scripts for running the JAMS Launcher and the JAMS Builder respectively
- **jams.exe, juice.exe**: Windows executable files for running the JAMS Launcher and the JAMS Builder respectively

The JAMS installation directory can easily be moved to other locations on the same or other computers, i.e. apart from a suited Java version there exist no external dependencies for running JAMS. However, while the starter scripts and executable files in the root of the JAMS installation directory will always work independently of the location of the directory, any Desktop and Start Menu shortcuts created with the Windows installer have to be adapted accordingly.
