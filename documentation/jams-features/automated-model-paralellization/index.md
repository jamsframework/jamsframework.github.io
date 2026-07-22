---
layout: doc
title: Automated Model Parallelization
section: JAMS Features
section_url: /documentation/#jams-features
---

## Overview

JAMS includes preprocessing capabilities that automatically modify models before execution. JAMS preprocessors are organized as a set of components that function as meta-models, applying automatic modifications to model data and structure rather than simulating environmental processes.

## Preprocessor Components

Preprocessors are standard JAMS components executed in a pre-processing phase. The preprocessor definition is integrated into the JAMS model itself.

<figure>
  <img src="{{ '/assets/img/documentation/jams-features/automated-model-paralellization/2020-04-24-09_22_49-Apache-NetBeans-IDE-11.0-1.png' | relative_url }}" alt="Pre-processor definition in a JAMS model">
  <figcaption>Figure 1: Pre-processor definition in a JAMS model</figcaption>
</figure>

## Primary Use Case: Model Parallelization

While preprocessors can be used for all kinds of model modifications, their most common and primary use case is the automated parallelization of a model. Figure 1 shows an example of such a preprocessor. Here, JAMS tells the `ConcurrentContextProcessor` (marked by "1") to be applied on the HRULoop (marked by "2"). It will basically do two things:

1. The overall set of HRUs will be split into n subsets, where n is the number of the computer's processor cores. These subsets are chosen such that they are spatially independent, i.e. there are no interactions between HRUs from two different subsets. This "segmentation" is done by a separate class which is given as a parameter, `EntityPartitioner` in this case (marked by "3"). `EntityPartitioner` will do two things:
   - It will generate all independent HRU subsets by identifying all HRUs that drain to a reach and then collect their respective sub-basins, i.e. all upstream HRUs.
   - Then, these subsets are joined into n groups of equal size.

   Another segmentation component is `SubbasinPartitioner`, which can be applied for multi-routing models and which makes use of the "subbasin" attribute generated for each HRU by WebHRU.

2. Once the n HRU subsets were created, the modification of the model structure starts. The `ConcurrentContextProcessor` will create n copies of the HRULoop with all of its components inside. Each of these n HRULoops will be assigned one of the n HRU subsets created in the last step. In addition, the n HRULoops will be put into a new "parent" context which allows to run its children in parallel. So during simulation, these n HRULoops will run at the same time within the current timestep. Once all are finished, the model moves on to the next time step. Since the time is as long as the longest running HRULoop, the HRU subsets need to be as equal in size as possible.

   During the duplication of HRULoops that are run in parallel, a few additional things need to be taken care of. The `SpatialWeightedSumAggregators` e.g. are summing up HRU values at a given time step. In order to avoid that two or more parallel `SpatialWeightedSumAggregators` interfere by writing to the same target variable (thereby overwriting each other's results), they have to be excluded from the parallel execution. These exclusions are defined by the "exclude_component" attribute (marked by "4"), which in this case lists also the routing components and the `AreaFraction` components.

## Performance Considerations

Once the parameters have been set for a specific model, this approach works for any region without manual interaction by the modeller. Unfortunately, due to the fact that only part of the model runs in parallel, the efficiency (i.e. the so-called *Speedup*) of the approach is not perfect. In a typical application, the model simulation time will be about 50% of the standard model when using 4 processor cores. In this case, the Speedup is 2, while the ideal Speedup would be 4. In order to provide control over the amount of processor cores used by the model, the percentage used can be controlled by a *scale_factor* (marked by "5", 1 means 100%).

## Configuration

Preprocessing can be disabled in the global JAMS configuration.
