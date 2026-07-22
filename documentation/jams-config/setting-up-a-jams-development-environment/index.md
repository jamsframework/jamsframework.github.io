---
layout: doc
title: Setting up a JAMS Development Environment
section: JAMS Setup & Configuration
section_url: /documentation/#jams-setup
---

## Introduction

This guide covers setting up a development environment for JAMS and its model libraries (e.g. J2K), for anyone who wants to build the latest source, implement custom model components, or modify JAMS itself. JAMS uses Git for version control and Maven for builds, so setup is IDE-agnostic — any IDE with Maven support (NetBeans, IntelliJ IDEA, Eclipse, VS Code) works.

### Recommended Software

1. A JDK, version 17 or newer (e.g. [OpenJDK](https://jdk.java.net))
2. Git
3. An IDE with Maven support, if you don't want to work from the command line

Maven itself does not need to be installed separately — both repositories include the Maven wrapper (`mvnw`/`mvnw.cmd`), which downloads the correct Maven version automatically.

## Downloading Sources

JAMS and its model libraries are hosted on GitHub:

```
git clone https://github.com/jamsframework/jams.git
git clone https://github.com/jamsframework/jamsmodels.git
```

## Building JAMS

```
cd jams
./mvnw install -pl jams-starter -am
```

This builds the `jams-starter` module and its dependencies, and installs the JAMS platform artifacts (`jams-api`, `jams-main`, …) into your local Maven repository so the model libraries can build against them. The runnable bundle is assembled in `jams-bin`:

```
cd jams-bin
./juice.sh
```

## Building the Model Libraries

With the JAMS build above already installed locally:

```
cd jamsmodels
./mvnw package                    # build all models
./mvnw package -pl J2K_base -am   # build a single model, e.g. J2K_base
```

The built model jars are collected in the `components/` directory of the `jamsmodels` checkout. Add that directory to the `libs` property of JAMS (Settings dialog in JUICE — see [JAMS System Configuration]({{ '/documentation/jams-config/jams-system-configuration/' | relative_url }})) so JAMS picks up the compiled components.

## Working in an IDE

Both `jams` and `jamsmodels` are plain multi-module Maven projects — open the checkout's root `pom.xml` in your IDE ("Open Project" / "Import Maven Project", depending on the IDE) and it will resolve modules and dependencies automatically. To develop a new model component, add it as a class in the relevant model module (or create a new Maven module for it) and implement the `JAMSComponent` interface — see the existing components in `jamsmodels` for examples.

## Running JAMS/J2K from the IDE

To run or debug JAMS from your IDE, set up a run configuration for the `jams-starter` module's main class with arguments such as:

```
-c <path to configuration file> -m <path to model definition file>
```

Run without arguments (or with `-h`/`--help`) to see all available options — see [Starting JAMS]({{ '/documentation/jams-config/starting-jams/' | relative_url }}) for the full list. After modifying model components, rebuild the affected `jamsmodels` module (see above) before running — JAMS loads components from the built jars, not directly from source.
