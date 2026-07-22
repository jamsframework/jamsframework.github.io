---
layout: doc
title: Inundation Model J2000-Flood
section: JAMS Models
section_url: /documentation/#jams-models
---

The J2000-flood model is an extension to the J2000 model with which it shares most of the components for the description of the hydrologic cycle. The flood simulation extension is characterized as a conceptual and easily transferable approach that is simultaneously not overly data and resource intensive, as well as easily parameterizable. This extension was developed with the goal of simulating floodplain/wetland inundation within the model. Due to the data scarcity typical of remote catchments, the extension's parameters (HRU elevation and river width) could be obtained from remote sensing data only.

On an iterative basis the water height in each river segment is compared to the elevation of its neighboring HRU. In case flooding occurs, the HRU floods its topological connected model entities, until the flood level is too low to spread any further. Technically the distributed water volume is stored in the exceeded depression storage, which interacts with soil and atmosphere.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/jams-models/inundation-model-j2000-flood/Flood comp J2000.png' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/inundation-model-j2000-flood/Flood comp J2000.png' | relative_url }}" alt="Flood component"></a>
    <figcaption>Schematic concept of a J2000(-Flood) model (left) including the inundation extension (right)</figcaption>
  </figure>
</div>

## Adaption of the J2000 towards the J2000-Flood

To apply the J2000-Flood modelling system the following components need to be replaced or added in the JAMS Builder:

1. Replace the JAMS component *StandardEntityReader* with the *StandardEntityReaderUpstreamTopo*, which adds a two-directional linkage between entities to define flood direction from each river segment.
2. Add the component *SubbasinFlooding* at the ende of the *ReachLoop*. In case of overflow of a river segment this component iterates over (elevation-sorted) HRUs and distributes the water as described above.
3. Add a *DoubleConditionalContext* in the *HRULoop* and include the original soil module as well as a second one to allow different parametrizations for flooded and non-flooded HRUs (configuration: if *floodVolume* is zero the soil module for non-flooded HRUs will be executed and the other way around).
4. Add the component *VariableAdder* at the the beginning of the *HRULoop* to add the *floodVolume* to the depression storage (outVar: *actDPS*), which will hold the flood water and interacts with ground and atmosphere. A duplication of the *VariableAdder* (place it just below) could be useful (outVar: *actDPS2*) to see the level of the depression storage (actual flood level) before it interacts with ground and atmosphere in each time step.
5. Make sure that all new variables (*floodVolume, actDPS2 ...*) are set to zero in the *ZeroSetter* and *CatchmentResetter* at the beginning of each time step. Add an additional *ZeroSetter* at the beginning of the *ReachLoop* to set *floodHeight* to zero.
6. For an useful output it might be good to a add various aggregators, for example to calculate the mean flood level only during flood season.

<div class="img-gallery">
  <figure>
    <a href="{{ '/assets/img/documentation/jams-models/inundation-model-j2000-flood/Juice_adaption_marked.png' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/inundation-model-j2000-flood/Juice_adaption_marked.png' | relative_url }}" alt="Adaptions in JAMS Builder"></a>
    <figcaption>Adaptions of the J2000 (left) towards the J2000-Flood (right) in JAMS Builder marked as above</figcaption>
  </figure>
</div>

## Application in the Upper Zambezi

- [Meinhardt, M., Kralisch, S., Fink, M., Fleischer, M., Zimba, H., Butchart-Kuhlmann, D., Phiri, W., Chabala, A., Trautmann, T., Helmschrot, J., & Nyambe, I. (2016). Process-based distributed hydrological modelling of annual floods in the Upper Zambezi using the Desert Flood Index. Poster at European Geosciences Union General Assembly (EGU), 17 - 22 April 2016, Vienna.](http://www.geoinf.uni-jena.de/~ra53mac/Poster_EGU_Meinhardt_et_Al_landscape.pdf)
- [Example video of HRU flooding](http://www.youtube.com/watch?v=rQoQlo4WDhI&t=6s)
