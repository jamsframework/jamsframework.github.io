---
layout: page
title: Downloads
description: "Download the latest JAMS release from GitHub, or build JAMS from source."
---

## Latest release

The ready-to-run bundle (JUICE, JAMS Launcher, model libraries and all dependencies included) is published on GitHub:

<div class="buttons" style="justify-content:flex-start; margin: 1.2rem 0;">
  <a class="btn primary" href="https://github.com/jamsframework/jams/releases/latest">Download latest release</a>
  <a class="btn" href="https://github.com/jamsframework/jams/releases">All releases</a>
</div>

Unpack the archive and run `juice.sh` / `juice.bat` — no installation required.

## System requirements

- **Building** JAMS from source requires a JDK 17 or newer (Maven and all third-party dependencies are included via the Maven wrapper).
- **Running** the pre-built bundle only requires a Java runtime, version 17 or newer. On macOS, use Java 24 or newer if you hit a rare accessibility-related crash (a JDK bug fixed in Java 24).

## Building from source

Clone and build the JAMS framework itself:

```
git clone https://github.com/jamsframework/jams.git
cd jams
./mvnw install -pl jams-starter -am
cd jams-bin && ./juice.sh
```

This builds and starts the JAMS framework itself, without any model components. To build the model libraries (e.g. the J2K family), also clone and build [jamsmodels](https://github.com/jamsframework/jamsmodels):

```
git clone https://github.com/jamsframework/jamsmodels.git
cd jamsmodels
./mvnw package                    # build all models
./mvnw package -pl J2K_base -am   # build a single model, e.g. J2K_base
```

The built model jars are collected in the `components/` directory of the jamsmodels checkout — add that directory to the `libs` property of JAMS (settings dialog in JUICE) and the models are ready to use.

## Version history

Release notes for past versions are collected on the [Changelog]({{ '/changelog/' | relative_url }}) page. Notes for new releases are published directly on [GitHub Releases](https://github.com/jamsframework/jams/releases).
