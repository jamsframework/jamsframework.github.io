---
layout: default
title: JAMS Modelling Framework
description: "JAMS is a pure-Java, open-source framework for building and applying modular environmental simulation models."
---

<header class="hero wrap">
  <span class="logo-chip"><img src="{{ '/assets/jams-logo.png' | relative_url }}" alt="JAMS logo"></span>
  <p class="tagline">
    A pure-Java, open-source framework for building and applying modular
    environmental simulation models.
  </p>
  <div class="buttons">
    <a class="btn primary" href="https://github.com/jamsframework/jams/releases/latest">Download JAMS</a>
    <a class="btn" href="https://github.com/jamsframework/jams">View on GitHub</a>
    <a class="btn" href="{{ '/documentation/' | relative_url }}">Documentation &amp; Wiki</a>
  </div>
</header>

<main class="wrap">

<section>
  <div class="cards">
    <div class="card">
      <h2>Modular by design</h2>
      <p>
        Models are assembled from reusable simulation components, wired
        together in an XML model definition — by hand or visually in the
        JUICE model editor. The framework handles the simulation life
        cycle, spatial and temporal iteration and parallel execution.
      </p>
    </div>
    <div class="card">
      <h2>From data to insight</h2>
      <p>
        Explore model output with the JADE data explorer, visualize
        spatial results on a 3D globe, and calibrate and analyze your
        models with the OPTAS optimization and sensitivity tools.
      </p>
    </div>
    <div class="card">
      <h2>Proven in practice</h2>
      <p>
        JAMS provides the process components behind the J2000 model
        family and has been used worldwide for simulating hydrological,
        nutrient transport and erosion processes.
      </p>
    </div>
  </div>
</section>

<section>
  <div class="start" id="getting-started">
    <h2>Getting started</h2>
    <p style="margin:0 0 0.8rem">
      The quickest way is the ready-to-run bundle from the
      <a href="https://github.com/jamsframework/jams/releases/latest">latest release</a>
      — unpack, run <code>juice.sh</code>/<code>juice.bat</code>, done
      (Java 17+ required). Building from source is just as easy:
    </p>
    <pre><code>git clone https://github.com/jamsframework/jams.git
cd jams
./mvnw install -pl jams-starter -am
cd jams-bin &amp;&amp; ./juice.sh</code></pre>
    <p>
      Building only requires a JDK 17+ (Maven and all third-party
      dependencies are included); running the bundle only needs a
      Java runtime, version 17 or newer. On macOS, use Java 24 or newer
      if you hit a rare accessibility-related crash (a JDK bug fixed in
      Java 24).
    </p>
    <h2 style="margin-top:1.6rem">Building the model libraries</h2>
    <pre><code># requires the JAMS build above (it installs the JAMS artifacts)
git clone https://github.com/jamsframework/jamsmodels.git
cd jamsmodels
./mvnw package                    # build all models
./mvnw package -pl J2K_base -am   # build a single model, e.g. J2K_base</code></pre>
    <p>
      The built model jars are collected in the <code>components/</code>
      directory of the jamsmodels checkout — add that directory to the
      <code>libs</code> property of JAMS (settings dialog in JUICE) and
      the models are ready to use.
    </p>
  </div>
</section>

</main>
