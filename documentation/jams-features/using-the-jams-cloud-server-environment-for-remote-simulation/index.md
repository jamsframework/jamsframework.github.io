---
layout: doc
title: Using the JAMS Cloud Server Environment for Remote Simulation
section: JAMS Features
section_url: /documentation/#jams-features
---

For complex models it is desirable to make use of parallel computing and highly performant computer hardware. While parallelization is available both for single and multiple simulations, the utilization of performant server hardware is often a problem.

Addressing this issue, JAMS features a client-server environment (JAMS Cloud) which provides the required components:

1. A stand-alone JAMS server environment with a RESTful interface provides functions to
   - upload a model (including workspace and model definition) and required component libraries from a JAMS desktop client to the server
   - run a simulation of that model on the server
   - control the simulation on the server (check state, interrupt)
   - download the model's workspace or individual files within (e.g. results only)
2. A graphical client for the JAMS server which is embedded in the JAMS model builder (JUICE)

In order to make use of the JAMS Cloud, you need access data for a JAMS Cloud server (i.e. its URL, a user name and password), the standard model builder and the model to be run on the server. For a typical remote modelling workflow, the following steps are required:

1. Open your model in JUICE and make sure that it would load and run locally. Start it and check for any error messages. If everything works as expected, stop the simulation. If you want to perform parameter sampling (e.g. for parameter calibration or sensitivity analyses), prepare your model beforehand — see [Parameter Sampling and Calibration]({{ '/documentation/jams-features/parameter-sampling-and-calibration/' | relative_url }}) for detailed information about setting up a sampling model.

2. Press the JAMS Cloud button from the toolbar menu to open the login window.

   <img src="{{ '/assets/img/documentation/jams-features/using-the-jams-cloud-server-environment-for-remote-simulation/img_593e5bd9bc0f3.png' | relative_url }}" alt="JAMS Cloud login window">

3. Provide information about
   - the server URL (1)
   - login user name (2)
   - login password (3)

   … and press OK.

   <img src="{{ '/assets/img/documentation/jams-features/using-the-jams-cloud-server-environment-for-remote-simulation/img_593e5cb674b73.png' | relative_url }}" alt="JAMS Cloud login fields">

4. Upload all required model data and libraries to the server and start the model simulation by pressing the "Run on cloud" button.

   <img src="{{ '/assets/img/documentation/jams-features/using-the-jams-cloud-server-environment-for-remote-simulation/img_593e5e735e4a5.png' | relative_url }}" alt="Run on cloud button">

   As a result, the client will synchronize the model workspace, the model definition and all required component libraries with the server. Depending on network bandwidth and whether the files have already been uploaded before or not, this process can take some time. After successful synchronization, the model will be started on the server and the user will be provided with the related job ID.

   <img src="{{ '/assets/img/documentation/jams-features/using-the-jams-cloud-server-environment-for-remote-simulation/img_593f87c145303.png' | relative_url }}" alt="Job ID after synchronization">

5. Check for your jobs and their execution state by pressing the "Browse JAMS cloud" button.

   <img src="{{ '/assets/img/documentation/jams-features/using-the-jams-cloud-server-environment-for-remote-simulation/img_593e5ee80e50f.png' | relative_url }}" alt="Browse JAMS cloud button">

   The JAMS cloud browser will show all your jobs (1) and uploaded workspaces (2). In the "Jobs" view, you will find your finished jobs (3) and your currently processed jobs (4). The jobs and workspaces are presented as a directory/file tree, allowing you to easily browse their contents.

   <img src="{{ '/assets/img/documentation/jams-features/using-the-jams-cloud-server-environment-for-remote-simulation/img_593e5fe9d5375.png' | relative_url }}" alt="JAMS cloud browser jobs view">

6. Select and right-click any single file or the job node to download it to your local machine.

   <img src="{{ '/assets/img/documentation/jams-features/using-the-jams-cloud-server-environment-for-remote-simulation/img_593e618379e14.png' | relative_url }}" alt="Download file context menu">

7. Select the "Kill" function from the job's context menu to interrupt a running job.

   <img src="{{ '/assets/img/documentation/jams-features/using-the-jams-cloud-server-environment-for-remote-simulation/img_593e62520b789.png' | relative_url }}" alt="Kill job context menu">
