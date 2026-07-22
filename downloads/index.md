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

```
git clone https://github.com/jamsframework/jams.git
cd jams
./mvnw install -pl jams-starter -am
cd jams-bin && ./juice.sh
```

Model libraries (e.g. the J2K family) are built the same way from the [jamsmodels](https://github.com/jamsframework/jamsmodels) repository — see the [homepage]({{ '/' | relative_url }}#getting-started) for the full getting-started walkthrough.

## Version history

Release notes for past versions are collected on the [Changelog]({{ '/changelog/' | relative_url }}) page. Notes for new releases are published directly on [GitHub Releases](https://github.com/jamsframework/jams/releases).
