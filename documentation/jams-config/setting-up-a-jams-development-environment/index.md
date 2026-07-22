---
layout: doc
title: Setting up a JAMS Development Environment
section: JAMS Setup & Configuration
section_url: /documentation/#jams-setup
---

## Introduction

The guide provides installation instructions for a JAMS/J2K development environment on Windows using Java 12, NetBeans IDE, and Tortoise SVN. These are examples; alternative tools and versions can be substituted. This resource targets users wishing to explore the latest JAMS software version or modeling components and implement custom extensions or modifications. While Windows is demonstrated, all steps apply to Linux or OS X systems using alternative SVN clients.

### Recommended Software

1. Java OpenJDK (https://jdk.java.net)
2. NetBeans IDE (https://netbeans.apache.org)
3. Tortoise SVN (https://tortoisesvn.net)

## Downloading Sources

JAMS sources and scripts are housed in a subversion (SVN) repository for file and directory version management. A valid SVN account accesses the JAMS-SVN; read-only access uses credentials "guest"/"guest". Setting up the development environment requires creating directories and populating them from the SVN repository.

1. Create directory for JAMS (example: c:\jams)
2. Create directory for JAMS models (example: c:\jamsmodels)
3. Right-click on c:\jams → SVN Checkout, entering `http://svn.geogr.uni-jena.de/svn/jams/trunk` as repository URL → OK
4. Right-click on c:\jamsmodels → SVN Checkout, entering `http://svn.geogr.uni-jena.de/svn/jamsmodels/trunk` as repository URL → OK

Alternatively, download latest source packages from the [Downloads](https://jams.uni-jena.de/downloads/) page.

## Downloading Test Data

The JAMS-SVN contains a repository with test datasets for various models. The modeldata repository contains substantial data; only specific sub-folders should be downloaded.

1. Create directory for model data (example: c:\jamsmodeldata)
2. Right-click on c:\jamsmodeldata → SVN Checkout, entering `http://svn.geogr.uni-jena.de/svn/modeldata` as repository URL (do not checkout yet)
3. Use the browse button (right of repository URL) to select desired data folders (hold CTRL for multiple selections) → OK

## Directory Structure

After these steps, directories for JAMS and JAMS models (and model data) exist. Beyond Java sources, the JAMS directory contains binary data and Ant scripts for compiling JAMS without NetBeans. Pre-configured NetBeans projects in the nbprojects subdirectory enable easy development environment setup.

The model directory contains sub-directories with Java sources from different model libraries, including components needed for creating JAMS models, plus an nbprojects folder with pre-configured NetBeans projects.

The data directory houses various model workspaces with model definitions and input data.

## Building JAMS and Models

### Building with Ant Scripts

Apache Ant controls the JAMS build procedure. IDE installation is not required; instead, Ant scripts at c:\jams\build\build.xml serve as entry points for command-line library compilation. Apache Ant installation (downloadable at http://ant.apache.org/bindownload.cgi) is prerequisite.

Creating JAMS libraries with Ant requires:

1. Open command line in c:\jams\build
2. Execute command `ant clean` to delete existing JAMS libraries
3. Execute command `ant dojams` to create all JAMS libraries

These steps can also be performed using c:\jams\build\clean.bat and c:\jams\build\build-jams.bat Windows batch files. Upon successful compilation, the c:\jams\jams-bin directory contains libraries with necessary system classes (lib subdirectory) and standard components (components subdirectory). Combined with external libraries in c:\jams\ext, they provide the JAMS API, runtime environment, and graphical user interfaces for model creation, execution, and result evaluation.

### Building with NetBeans

#### JAMS

Pre-configured NetBeans projects are stored in c:\jams\nbprojects. To open them, select File → Open Project and choose the desired JAMS sub-project from c:\jams\nbprojects. To compile all JAMS sources, open the "jams-starter" project, right-click on "jams-starter," and choose Clean and Build. This creates all necessary libraries and automatically copies them to c:\jams\jams-bin.

#### Models (e.g. J2K)

Many models (J2K, J2K-S, J2Kg) include pre-configured NetBeans projects in the SVN repository. To open them, select File → Open Project and choose the desired project from c:\jamsmodels\nbprojects. If the "Reference Problems" dialog appears, use "Resolve Problems…" to specify storage locations for "jams-api.jar" and "jams-main.jar" libraries found in the JAMS library folder (e.g., c:\jams\jams-bin\lib). After compiling, resulting libraries are stored in c:\jamsmodels\nbprojects\components or the dist subfolder of the model's project folder (e.g., c:\jamsmodels\nbprojects\J2K_base\dist).

For models without pre-configured projects:

1. In NetBeans: File → New Project → Java Project with Existing Sources
2. Indicate project name (e.g., J2K) and directory (e.g., c:\jamsmodels\nbprojects\J2Kg, where compiled classes and JAR file are stored) → Next
3. Source Package Folder → Add Folder… → c:\jamsmodels\J2Kg\src → OK
4. Press Finish
5. Include libraries: right-click on J2Kg/Libraries → Add JAR/Folder… and select JAMS libraries jams-api.jar and jams-main.jar from c:\jams\jams-bin\lib
6. Right-click on J2Kg → Clean and Build (compiles project and creates J2Kg.jar in c:\jamsmodels\nbprojects\J2Kg\dist\)

#### Template for JAMS Components

A component template for NetBeans is found at c:\jams\template\JAMSComponent.java. NetBeans integration:

1. Tools → Templates → Java → Add…
2. Select the file → Add

Afterwards, "JAMSComponent" is available as a file type when creating a new class.

## Running JAMS/J2K

To run JAMS, select the jams-starter project as the main project (Run → Set Main Project in the NetBeans menu). The jams-starter project contains no Java sources but serves as an entry point for building and starting JAMS. It includes three predefined starter configurations:

1. *CmdLine*: run JAMS in command line mode without GUI
2. *JAMS Launcher*: run the JAMS Launcher GUI to load and run models
3. *JUICE*: run the JAMS Builder to create, load, configure, and run models

Select configurations using the drop-down box in the NetBeans toolbar. Start the project using F6, the green start button, or right-click context menu (right-click jams-starter → Run). Modify startup arguments as follows:

1. Right-click jams-starter → Properties → Run
2. Under "Arguments," insert: `-c <complete path of configuration file> -m <complete path of model definition file>`. Valid arguments display in default output when using -h or --help arguments.

In default configuration, the JAMS Launcher or JUICE opens. From either interface, load a model via File → Load model.

Most model execution requires additional libraries (e.g., J2K_base.jar, J2K_ext.jar, and jams-components.jar). Via Edit → Change settings… in JAMS, specify additional libraries for model execution consideration. Settings automatically save when closing JAMS in the JAMS system configuration.

Note: After modifying model components, the JAR file always has to be re-generated with the components before execution (Step 6 in "Building JAMS and Models" above)!
