---
layout: doc
title: Water and Nutrient Balance Model J2000-S
section: JAMS Models
section_url: /documentation/#jams-models
math: true
---

The water and nutrient balance model J2000-S offers a simulation of the water and nitrogen balance of meso scale catchment areas. The model is an extension to the [J2000](http://jams.uni-jena.de/ilmswiki/index.php/Hydrological_Model_J2000) model with which it shares most of the components for the description of the hydrologic cycle. The additional components, soil temperature, soil nitrogen balance, land use management, plant growth as well as ground water nitrogen balance, are described for the specification of the nitrogen balance. Further modules are adapted for the demands of the nitrogen balance.

## Soil Nitrogen Module

The description of the soil nitrogen balance is carried out similarly to the SWAT model (Arnold et al. 1998). Within the individual soil horizons the five nitrogen pools for nitrate, ammonium, stable organic substances, active organic substance and fresh plant remains as biomass are distinguished. The fluxes and transformations between the pools and outside the soil, like nitrification, denitrification, mineralization, volatilation, plant uptake and eluviation, are calculated via the empirical relations against the soil humidity and soil temperature. The nitrogen flux is passed as well as the water transport via a routing method between the subareas to the receiving stream (see figure 1).

The nitrogen input caused by fertilization and Bestandesabfall as well as the removal through the plants is provided by the plant growth module and the land use management module. The mineral inputs are allocated to the ammonium pool or directly to the nitrate pool. The organic nitrogen is either allocated to the Bestandesabfall pool or the active organic pool. The latter is poised with the stable organic pool. The nitrate pool is the central allocation section for the discharge as eluviation, plant uptake and denitrification. The processes described in the module take place in free parameterizable soil horizons. Here, the delivery of organic substances and fertilizer as well as the removal of nitrogen with the surface runoff are limited to the top horizon.

<figure>
  <a href="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Bodenstickstoffmodul.jpg' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Bodenstickstoffmodul.jpg' | relative_url }}" alt="Bodenstickstoffmodul"></a>
  <figcaption>Figure 1: Structure of the soil nitrogen module</figcaption>
</figure>

The here applied nitrogen module contains some simplifications. Thus, no plant uptake from the ammonium pool is offered. Furthermore, the decomposition of organic substances is directly simulated to nitrate without any detour via ammonium. The N immobilization from mineral to organic nitrogen in the soil zone is neglected completely. The water transport of nitrogen is shown very generalized. Thus, a complete mixing of nitrogen in the individual storages takes place instead of advection and dispersion. The individual processes are described in the model as follows:

### Plant Uptake

At first, the plant's demands (potential plant uptake) which shall be met by the soil nitrogen storage on the day t0 are generated:

$$
potNup= BioNopt - BioN \!
$$
[1]

with:

*$$potNup\!$$ = potential plant uptake [kgN/ha]*

*$$BioNopt\!$$ = optimal biomass [kgN/ha]*

*$$BioN\!$$ = actual biomass [kgN/ha]*

Afterwards, the proportions of the soil horizons which lie within the effective root zone are generated. At this, the horizons which lie entirely within the root zone are taken into account completely (partroot = 1). However, the horizon which lies only partly in the root zone is only considered partly:

$$
partroot[i] =  \frac {rootdepth - layerdepth[i - 1]}{layerdepth[i] - layerdepth[i - 1]} \!
$$
[2]

with:

*$$i\!$$ = horizon [-]*

*$$partroot\!$$ = proportion of the horizon at the root zone [-]*

*$$layerdepth\!$$ = lower threshold of soil horizon [-]*

The allocation of the n-uptake to the individual horizons is carried out against a calibration parameter ($$\beta_{Ndist}\!$$). At this, the potential uptake for the individual horizons is calculated:

$$
potNup_z[i] = \frac {potNup} {1 - \exp(-\beta_{Ndist})} \cdot \left(1 - \exp\left(-\beta_{Ndist} * \frac {layerdepth[i]} {rootdepth}\right)\right) - uptake[i-1]
$$
[3]

with:

*$$i\!$$ = horizon [-]*

*$$partroot\!$$ = proportion of the horizon at the root zone [-]*

*$$layerdepth\!$$ = lower threshold of the soil horizon [-]*

*$$potNup\!$$ = potential plant uptake [kgN/ha]*

*$$potNup_z\!$$ = potential plant uptake in the individual horizons [kgN/ha]*

*$$uptake\!$$ = potential plant uptake which has been taken from upper horizons already [kgN/ha]*

*$$\beta_{Ndist}\!$$ = distribution parameter of the plant uptake; default value = 1.0; possible values 1 - 15 [-]*

For the calculation of the potential plant uptake which is met by upper horizons already, the following connection is applied:

$$
uptake = uptake + potNup_z[i] \!
$$
[4]

*$$potNup_z\!$$ = potential plant uptake in the individual horizons [kgN/ha]*

*$$uptake\!$$ = potential plant uptake which has been taken from upper horizons already [kgN/ha]*

The calculation of a demand is carried out according to the following equation:

$$
demand = (NO_3Pool[i] \cdot partroot[i]) - potNup_z[i] \!
$$
[5]

with:

*$$i\!$$ = horizon [-]*

*$$partroot\!$$t = proportion of the horizon of the root zone [-]*

*$$demand\!$$ = demand that can be met by the soil nitrogen pool [kgN/ha]*

*$$NO_3Pool\!$$ = soil nitrogen pool [kgN/ha]*

*$$potNup_z\!$$ = potential plant uptake in the individual horizons [kgN/ha]*

If this demand is greater than 0, it can be met by the existing nitrogen storage with:

$$
NO_3Pool2[i] =
\begin{cases}
NO_3Pool1[i] - potNup_z[i] & \mathrm{f\ddot{u}r} \; \; demand >= 0 \\
NO_3Pool1[i] - (NO_3Pool1[i] \cdot partroot[i])& \mathrm{f\ddot{u}r} \; \; demand < 0
\end{cases}
$$

and

$$
demand =
\begin{cases}
demand[i] = 0  & \mathrm{f\ddot{u}r}\; \; demand >= 0 \\
demand[i] = demand &\mathrm{f\ddot{u}r} \; \; demand < 0
\end{cases}
$$

with

*$$i\!$$ = horizon [-]*

*$$demand\!$$ = demand that can be met by the soil nitrogen pool [kgN/ha]*

*$$NO_3Pool1\!$$ = soil nitrate pool before the time step [kgN/ha]*

*$$NO_3Pool2\!$$ = soil nitrate pool after the time step [kgN/ha]*

*$$potNupz\!$$ = potential plant uptake in the individual horizons [kgN/ha]*

*$$partroot\!$$ = proportion of the horizon of the root zone [-]*

Afterwards, the actual plant uptake can be calculated on the basis of the potential plant uptake and the demand that has been summed up via the horizons:

$$
N_{uptake} = potNup + \sum^{n}_{i=1}{demand[i]}  \!
$$
[10]

with

*$$i\!$$ = horizon [-]*

*$$n\!$$ = number of horizons in the root zone [-]*

*$$demand\!$$ = demand which can be met by the soil nitrogen pool [kgN/ha]*

*$$potNup\!$$ = potential plant uptake [kgN/ha]*

*$$N_{uptake}\!$$ = actual plant uptake [kgN/ha]*

### Nitrate Rising by Evaporation

Soil water from deeper layers is transported into upper horizons via the evaporation flux. This happens for each horizon according to the SWAT method:

$$
n_{upmove} = 0.1 \cdot NO_3Pool \cdot \frac {aEvap} {act_{LPS} + act_{MPS} + sto_{FPS}} \!
$$
[1]

with

*$$n_{upmove}\!$$ = amount of nitrogen from the individual horizon which is transported by evaporation [kgN/ha]*

*$$NO_3Pool\!$$ = soil nitrogen pool [kgN/ha]*

*$$aEvap\!$$ = actual evapotranspiration of the horizon [l]*

*$$act_{LPS}\!$$ = actual large pore storage of the horizon [l]*

*$$act_{LPS}\!$$ = actual middle pore storage of the horizon [l]*

*$$sto_{FPS}\!$$ = fine pore storage of the horizon [l]*

### Transformation Processes in the Soil

#### Nitrification and Ammonium Volatilation

The transformation processes of the ammonium pool in this model are the nitrification from ammonium to nitrate and the ammonium volatilation. The calculation of the total transformation of the ammonium pool is carried out for both processes together. Afterwards, the rates for both processes are separated. In order to represent the influence of the temperature, the following coefficient needs to be calculated:

$$
\eta_{temp} = 0.41 \cdot \frac {temp_{Layer} - 5} {10}\!
$$
[1]

with

*$$\eta_{temp}\!$$ = soil temperature coefficient [-]*

*$$temp_{Layer}\!$$ = temperature of the soil layer [°C]*

The influence of the soil humidity on the nitrification is described via the coefficient eta_water:

for $$act_{LPS} + act_{MPS} < 0.25 \cdot (sto_{LPS} + sto_{MPS})\!$$

$$
\eta_{water} = \frac{act_{LPS} + act_{MPS} + sto_{FPS}} {0.25 \cdot (sto_{LPS} + sto_{MPS} + sto_{FPS})} \!
$$
[2]

for $$act_{LPS} + act_{MPS} >= 0.25 \cdot (sto_{LPS} + sto_{MPS}) \!$$

$$
\eta_{water} = 1 \!
$$
[3]

with

*$$\eta_{water}\!$$ = soil humidity coefficient [-]*

*$$sto_{LPS}\!$$ = maximum large pore storage of the horizon [l]*

*$$sto_{MPS}\!$$ = maximum middle pore storage of the horizon [l]*

*$$sto_{FPS}\!$$ = maximum fine pore storage of the horizon [l]*

*$$act_{LPS}\!$$ = actual large pore storage of the horizon [l]*

*$$act_{MPS}\!$$ = actual middle pore storage of the horizon [l]*

The dependency of the ammonium volatilation on the soil depth is calculated with the following equation:

$$
\eta_{vol_z} = 1 - \frac {layerdepth} {layerdepth + \exp (4.706 - (0.305 \cdot \frac {layerdepth}{20}))}\!
$$

*$$\eta_{vol_z}\!$$ = soil depth coefficient [-]*

*$$layerdepth\!$$ = layer depth of the horizon [cm]*

The Gesamtumsatz of the ammonium pool can be calculated as follows:

$$
N_{nit + vol} = NH_4Pool * (1 - \exp(-(\eta_{water} \cdot \eta_{temp})-(\eta_{vol_z} \cdot \eta_{temp})))\!
$$

This Gesamtumsatz is then distributed into:

$$
frac_{nitr} = 1 - \exp(-(\eta_{water} \cdot \eta_{temp}))\!
$$

$$
frac_{vol} = 1 - \exp(-(\eta_{vol_z} \cdot \eta_{temp}))\!
$$

$$
nitri_{trans} =  (frac_{nitr} /(frac_{nitr} + frac_{vol})) \cdot N_{nit + vol} \!
$$

$$
volati_{trans} =  (frac_{vol} /(frac_{nitr} + frac_{vol})) \cdot N_{nit + vol} \!
$$

with

*$$\eta_{water} \!$$ = soil humidity coefficient [-]*

*$$\eta_{temp}\!$$ = soil temperature coefficient [-]*

*$$\eta_{vol_z}\!$$ = soil depth coefficient [-]*

*$$NH_4Pool\!$$ = soil humidity coefficient [kgN/ha]*

*$$N_{nit + vol}\!$$ = Gesamtumsatz of the ammonium pool [kgN/ha]*

*$$frac_{nitr}\!$$ = fraction nitrification [-]*

*$$frac_{vol}\!$$ = fraction ammonium volatilation [-]*

*$$nitri_{trans}\!$$ = amount of nitrification [kgN/ha]*

*$$volati_{trans}\!$$ = amount of ammonium volatilation [kgN/ha]*

#### Pre-calculation for the Influence of Environmental Conditions

In order to show the influence of the soil temperature and soil humidity in the different transformation processes, the following coefficients need to be calculated beforehand:

$$
\gamma_{temp} = 0.9 \cdot \frac {temp_{Layer}} {temp_{Layer} \cdot \exp(9.93 - 0.312 \cdot temp_{Layer}} + 0.1 \!
$$
[1]

with

*$$\gamma_{temp}\!$$ = soil temperature coefficient [-]*

*$$temp_{Layer}\!$$ = temperature of the soil layer [°C]*

$$
\gamma_{water} =  \frac {act_{LPS} + act_{MPS} + sto_{FPS}} {sto_{LPS} + sto_{MPS} + sto_{FPS})} \!
$$
[2]

with

*$$\gamma_{water}\!$$ = soil humidity coefficient [-]*

*$$sto_{LPS}\!$$ = maximum large pore storage of the horizon [l]*

*$$sto_{MPS}\!$$ = maximum middle pore storage of the horizon [l]*

*$$sto_{FPS}\!$$ = maximum fine pore storage of the horizon [l]*

*$$act_{LPS}\!$$ = actual large pore storage of the horizon [l]*

*$$act_{MPS}\!$$ = actual middle pore storage of the horizon [l]*

#### Transfer between the Organic Pools

The transfer between the active and the stable organic pool can be calculated with the following equation:

$$
N_{Hum_{trans}} = \beta_{trans} \cdot (N_{activ_{pool}} \cdot (\frac{1} {fr_{actN}} -1) - N_{stabel_{pool}})\!
$$

with

*$$N_{Hum_{trans}}\!$$ = transfer rate between the active and stable organic pool [kgN/ha]*

*$$\beta_{trans}\!$$ = transfer constant between the active and stable organic pool; default value= 0.00001 [-]*

*$$N_{activ_{pool}}\!$$ = active organic pool [kgN/ha]*

*$$N_{stabel_{pool}}\!$$ = stable organic pool [kgN/ha]*

*$$fr_{actN}\!$$ = fraction of the organic nitrogen in the active organic pool = 0.02 [-]*

The transfer rate is here subtracted from the active pool whereas it is added to the stable pool.

#### Mineralization of the Active Pool

The active pool is mineralized to nitrate directly without taking the nitrification into account. The rate is calculated as follows:

$$
N_{actmin} = \beta_{min} \cdot \sqrt{\gamma_{temp} \cdot \gamma_{water}} \cdot N_{activ_{pool}}\!
$$

with

*$$N_{actmin}\!$$ = transfer rate between the active organic and the nitrate pool [kgN/ha]*

*$$\beta_{min}\!$$ = transfer constant between the active organic and the nitrate pool; default value = 0.002 [-]*

*$$N_{activ_{pool}}\!$$ = active organic pool [kgN/ha]*

*$$\gamma_{water}\!$$ = soil humidity coefficient [-]*

*$$\gamma_{temp}\!$$ = soil temperature coefficient [-]*

The transfer rate is subtracted from the active pool whereas it is added to the nitrate pool.

#### Dynamics of the Residue Pools

The dynamics of the decomposition of fresh organic substances (residue) from plant remains and organic fertilizer is carried out only in the top horizon. The residue are divided in two pools: the first one represents the biomass as a whole, the second represents the residue's amount of nitrogen. The supply to the residue pools is carried out via plant remains after the harvest and via the organic fertilization with the help of the following equation:

$$
Residue_{pool} = Residue_{pool} + inp_{biomass} + (fertorgN_{fresh} \cdot 10)\!
$$

$$
N_{residue_{pool}} = N_{residue_{pool}} + inpN_{biomass} + fertorgN_{fresh}\!
$$

with

*$$Residue_{pool}\!$$ = residue pool [kg/ha]*

*$$inp_{biomass}\!$$ = inputted biomass [kg/ha]*

*$$fertorgN_{fresh}\!$$ = inputted nitrogen via organic fertilization [kgN/ha]*

*$$N_{residue_{pool}}\!$$ = residue pool's amount of nitrogen [kgN/ha]*

The decomposition of the residue pool is carried out against the carbon-nitrogen relation (C/N-relation). The calculation of the C/N-relation is carried out according to the following equation.

$$
\epsilon_{C/N} = \frac{Residue_{pool} \cdot 0.58} {N_{residue_{pool}} + NO_3Pool}
$$

$$
\gamma_{ntr} = min
\begin{cases}
\exp(-0.693 \cdot\frac{\epsilon_{C/N} - 25} {25})\\
1.0
\end{cases}
$$

with

*$$\epsilon_{C/N}\!$$ = C/N-relation [-]*

*$$\gamma_{ntr}\!$$ = residue decomposition factor [-]*

*$$Residue_{pool}\!$$ = residue pool [kg/ha]*

*$$NO_3Pool\!$$ = nitrate pool [kgN/ha]*

*$$N_{residue_{pool}}\!$$ = residue pool's amount of nitrogen [kgN/ha]*

The decomposition constant of the residue pool is calculated with $$\gamma_{ntr}$$, $$\gamma_{water}$$, $$\gamma_{temp}$$:

$$
\delta_{ntr} = \beta_{rsd} \cdot \gamma_{ntr} \cdot \sqrt{\gamma_{water} \cdot \gamma_{temp}}\!
$$

with

*$$\delta_{ntr}\!$$ = constant of the residue decomposition's rate [-]*

*$$\gamma_{ntr}\!$$ = residue decomposition factor [-]*

*$$\beta_{rsd}\!$$ = residue decomposition coefficient; default value = 0.05 [-]*

*$$\gamma_{water}\!$$ = soil humidity coefficient [-]*

*$$\gamma_{temp}\!$$ = soil temperature coefficient [-]*

The decomposition of the residue pool is carried out with the constant of the residue decomposition's rate. At this, the nitrogen part is allocated to the active organic pool, in terms of humification, and the nitrate pool, in terms of mineralization, in a ratio of 20:80.

$$
Residue_{pool}2 = Residue_{pool}1 - (\delta_{ntr} \cdot Residue_{pool}1)\!
$$

$$
N_{active_{pool}}2 = N_{active_{pool}}1 + (0.2 \cdot \delta_{ntr} \cdot N_{residue_{pool}}1)\!
$$

$$
NO_3Pool2 = NO_3Pool1 + (0.8 \cdot delta_ntr \cdot N_{residue_{pool}}1)\!
$$

$$
N_{residue_{pool}}2 = N_{residue_{pool}}1 - (\delta_{ntr} \cdot N_{residue_{pool}}1)\!
$$

with

*$$\delta_{ntr}\!$$ = constant of the residue decomposition's rate [-]*

*$$Residue_{pool}1\!$$ = residue pool before the time step [kgN/ha]*

*$$Residue_{pool}2\!$$ = residue pool after the time step [kgN/ha]*

*$$N_{active_{pool}}1\!$$ = active organic pool before the time step [kgN/ha]*

*$$N_{active_{pool}}2\!$$ = active organic pool after the time step [kgN/ha]*

*$$NO_3Pool1\!$$ = soil nitrate pool before the time step [kgN/ha]*

*$$NO_3Pool2\!$$ = soil nitrate pool after the time step [kgN/ha]*

*$$N_{residue_{pool}}1\!$$ = residue pool's amount of nitrogen before the time step [kgN/ha]*

*$$N_{residue_{pool}}2\!$$ = residue pool's amount of nitrogen after the time step [kgN/ha]*

#### Denitrification

Denitrification occurs when the soil is nearly water-saturated. The rate depends on the amount of organic carbon in the soil as well as on the soil temperature. In comparison to SWAT (0,95), the degree of water saturation is lower (0.91) when denitrification occurs. This is because SWAT - in contrast to J2000 - does not consider the soil's air capacity. Thus, the underlying pore volume for the calculation of water saturation is higher in J2000. Furthermore, it is ensured that the rate is at the most 1 kgN/ha*d since higher rates are not expected in open land.

$$
denit_{trans} =
\begin{cases}
NO_3Pool \cdot (1 - \exp(-1.4 \cdot \gamma_{temp} \cdot C_{org}))& \mathrm{f\ddot{u}r} \; \; \gamma_{water} \ge \beta_{denit} \\
0.0  & \mathrm{f\ddot{u}r}\; \; \gamma_{water} < \beta_{denit}
\end{cases}
$$

with

*$$NO_3Pool\!$$ = soil nitrate pool [kgN/ha]*

*$$denit_{trans}\!$$ = denitrification rate [kgN/ha]*

*$$\gamma_{water}\!$$ = soil humidity coefficient [-]*

*$$\gamma_{temp}\!$$ = soil temperature coefficient [-]*

*$$\beta_{denit}\!$$ = denitrification coefficient; default value = 0.91 [-]*

### Mass Transport with Water Movement in the Soil

#### Nitrogen Concentration of Mobile Water

For the simulation of the mass transport caused by water movement, the nitrogen concentration of the mobile water is defined. Here, it is simplified assumed that only the nitrogen of the nitrate pool is mobile and therefore is taken into account for the calculation. The amount of water is determined on the basis of the soil storages and the water streams that leave the horizon.

$$
soil_{water} = act_{LPS} + act_{MPS} + sto_{FPS}\!
$$

$$
mobile_{water} =
\begin{cases}
(RD1_{out} * Beta_{NO_{3}}) + RD2_{out} + h_{perco} + hor_{by_{infilt}} + diff_{out} & \mathrm{f\ddot{u}r} \; \; Horizont = 1 \\
RD2_{out} + h_{perco} + hor_{by_{infilt}} + diff_{out}& \mathrm{f\ddot{u}r} \; \; i > Horizont < n\\
RD2_{out} + h_{perco} + diff_{out}& \mathrm{f\ddot{u}r} \; \; Horizont = n
\end{cases}
$$

$$
concN_{mobile} = \frac {NO_3Pool * (1 - \exp \frac{- mobile_{water}}  {(1 - \theta_{nit}) * soil_{water}})}  {mobile_{water}}
$$

with

*$$NO_3Pool\!$$ = soil nitrate pool [kgN/ha]*

*$$soil_{water}\!$$ = soil water [mm]*

*$$mobile_{water}\!$$ = amount of mobile water [mm]*

*$$\Beta_{NO_{3}}\!$$ = percolation coefficient; default value = 0.2 [-]*

*$$RD1_{out}\!$$ = surface runoff [mm]*

*$$RD2_{out}\!$$ = interflow [mm]*

*$$h_{perco}\!$$ = percolation in deeper horizons or ground water [mm]*

*$$hor_{by_{infilt}}\!$$ = infiltration water that goes into deeper layers in a time step and therefore passes by the actual horizon [mm]*

*$$diff_{out}\!$$ = water that leaves the horizon via diffusion [mm]*

*$$\theta_{nit}\!$$ = fraction of the pore volume from which anions are excluded (due to positive charge preponderance of the clay mineral); default value = 0.05 [-]*

*$$concN_{mobile}\!$$ = nitrogen concentration of the mobile water [kgN/ha*mm]*

The influence of the water that expands into deeper horizons in a time step is determined with a parameter ($$infil_{conc_{factor}}$$). At this, the parameter represents to what extend the bypass water interacts with the soil matrix or bypasses the layers that are flown through in macro pores.

$$
hor_{by_{infilt}}[i-1] = \sum^{n}_{i}{hor_{by_{infilt}}} * infil_{conc_{factor}}  \!
$$

with

*$$hor_{by_{infilt}}\!$$ = infiltration water that goes into deeper layers in a time step and therefore passes by the actual horizon [mm]*

*$$infil_{conc_{factor}}\!$$ = bypass parameter [mm]*

*$$i\!$$ = actual horizon [-]*

*$$n\!$$ = number of horizons [-]*

#### Nitrogen Transport in the Runoff Components

For the individual horizons the nitrogen loads for the runoff components are calculated on the basis of the mobile water's nitrogen concentration. At this, the interflow is considered in all horizons whereas the surface runoff is only considered in the top horizon. However, the percolation occurs in the deeper horizons or in the ground-water reservoir.

$$
N_{surface} = Beta_{NO_3} \cdot RD1_{out} \cdot concN_{mobile}\!
$$

$$
N_{interflow} = RD2_{out} \cdot concN_{mobile}\!
$$

$$
N_{perco} = (hor_{by_{infilt}} + h_{perco}) \cdot concN_{mobile}\!
$$

with

*$$concN_{mobile}\!$$ = nitrogen concentration of the mobile water [kgN/ha*mm]*

*$$hor_{by_{infilt}}\!$$ = infiltration water that goes in deeper layers and thus bypasses the actual horizon in a time step [mm]*

*$$N_{surface}\!$$ = nitrogen in the surface runoff [kgN/ha]*

*$$N_{interflow}\!$$ = nitrogen in the interflow [kgN/ha]*

*$$N_{perco}\!$$ = nitrogen in the percolation water [kgN/ha]*

*$$RD1_{out}\!$$ = surface runoff [mm]*

*$$RD2_{out}\!$$ = interflow [mm]*

*$$h_{perco}\!$$ = percolation [mm]*

*$$Beta_{NO_3}\!$$ = percolation coefficient [-]*

The percolation coefficient represents a measurement for the interaction of the surface runoff and the soil matrix of the top horizon and therefore determines the surface runoff's amount of nitrogen.

The material that leaves the horizon with the diffusion water can be calculated as follows: the water movement that occurs above the field capacity due to potential gradients is called diffusion. Here, a negative value for the diffusion water means a downward water movement whereas a positive value represents an upward water movement.

$$
diffoutN =
\begin{cases}
w_{l_{diff}}[i] * ConcN_{mobile}[i] & \mathrm{f\ddot{u}r} \; \; w_{l_{diff}} < 0 \\
w_{l_{diff}}[i] * ConcN_{mobile}[i+1] & \mathrm{f\ddot{u}r} \; \; w_{l_{diff}} < 0
\end{cases}
$$

and

$$
NO_3Pool[i] = NO_3Pool[i] + diffoutN \!
$$

and

$$
NO_3Pool[i+1] = NO_3Pool[i+1] - diffoutN \!
$$

with

*$$concN_{mobile}\!$$ = nitrogen concentration of the mobile water [kgN/ha*mm]*

*$$diffoutN \!$$ = nitrogen in the diffusion water [kgN/ha]*

*$$NO_3Pool\!$$ = soil nitrate pool [kgN/ha]*

*$$w_{l_{diff}}\!$$ = diffusion water [mm]*

*$$i\!$$ = soil horizon [kgN/ha]*

## Soil Temperature Module

The soil temperature is an important measurement for the matter regime modeling. Especially microbiological processes such as nitrification, denitrification and the transformation of organic nitrogen in the soil zone is strongly influenced by the prevailing temperature. In the here developed model J2K-S the soil temperature also plays an important role for the calculation of the following processes (see [Soil Nitrogen Module](#soil-nitrogen-module)):

- nitrification
- volatilation
- transformation of organic substance
- decomposition of plant remains
- denitrification

*Structure of the Module*

The soil temperature is simulated according to the empirical routines of SWAT (Arnold et al. 1998) and EPIC (Williams et al. 1984). At first, a surface soil temperature is generated for bare ground on the basis of the air temperature and insolation. This surface temperature is modified by attenuation factors that describe the effect of biomass and snow. The temperature of the different soil horizons is generated as upper boundary condition between the surface soil temperature and the long lasting mean temperature as lower boundary condition. At this, the attenuation effect of the soil is defined in consideration of the soil humidity and the bulk density. The equations of the individual processes can be found in Neitsch et al. (2002).

<figure>
  <a href="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Bodentemperaturmodul.jpg' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Bodentemperaturmodul.jpg' | relative_url }}" alt="Bodentemperaturmodul"></a>
  <figcaption>Figure 1: Structure of the soil temperature model</figcaption>
</figure>

Figure 2: Results of the soil temperature modeling for the surface area and at 40 cm depth at an investigated slope near Zeulenroda (Thuringia). *(the corresponding figure image is missing from the source wiki and could not be migrated)*

This figure shows the measured and modeled temperature at the surface (upper figure) as well as at 40 cm depth (lower figure) for an investigated area near the dam Zeulenroda. It can be seen that the temperature curve can be followed quite well in spite of certain deviations. This is emphasized by the high coefficient of determination of about 0.95.

## Plant Growth Module

The description for the simulation of plant growth is important for numerous hydrological mass transport processes, e.g. for the interception or the nitrogen uptake by the canopy. Plant growth is usually controlled via the simulation of the leaf area development (LAI) as well as the light interception and the transformation into biomass and is carried out according to SWAT (Arnold et al. 1998). At this, it is assumed that a potential plant growth, i.e. under optimum conditions, exists which is then modified in consideration of stress factors.

*Temperature Development and Heat Units*

The most important factor that determines the canopy's development is the temperature whose parameters are different for each plant. Therefore, each plant possesses a basis temperature that needs to be reached in order to activate a certain growth. The growth increases until the optimum temperature is reached and decreases noticeably when the maximum temperature is exceeded. The plant-specific growth development is carried out via the generating of heat units (=HU). The underlying hypothesis for this is the assumption that plants have a specific heat demand that is quantifiable until the necessary maturity state for the harvest is reached. An 'HU' is defined as a phenological effective temperature unit. An HU results from the daily accumulated daily average temperature that lies above the plant-specific basis temperature. Assumed that a maize plant has a basis temperature of 7° C and is exposed to a daily temperature of 15° C, its HU would be calculated as follows: 15 – 7 = 8 HUs. In this way, the individual heat unit developments are simulated for each land use type in consideration of the time of the sowing and harvest as well as the daily average temperature. The development of the root growth and the leaf area index is controlled via the heat unit development. At this, it is assumed that the plants invest their energy into the leaf development and the root growth. This simplified view also means that the development of leafs and roots is independent on water and nutrient supply. Furthermore, the plant's degree of maturity which influences the amount of nitrogen in the biomass is exclusively controlled via the temperature sum.

*Biomass Development*

The biomass development is simulated as potential biomass at first. At this, the photosyntetic radiation is the controlling unit for the biomass development. Thus, a potential biomass increase is generated for each day with the help of the radiation and leaf area (see figure 1).

<figure>
  <a href="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenwastumsmodul1.jpg' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenwastumsmodul1.jpg' | relative_url }}" alt="Pflanzenwastumsmodul1"></a>
  <figcaption>Figure 1: Structure of the plant growth module</figcaption>
</figure>

This daily biomass increase is reduced to the actual biomass increase with the help of stress factors, which are nitrogen supply, temperature and water supply (see figure 2).

<figure>
  <a href="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenwastumsmodul2.jpg' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenwastumsmodul2.jpg' | relative_url }}" alt="Pflanzenwastumsmodul2"></a>
  <figcaption>Figure 2: Structure of the growth's stress</figcaption>
</figure>

The stress factor that has the strongest effects at a point in space and time determines the actual biomass according to the principle of limiting factors. This, in turn, influences the nitrogen demand.

## Land Use Management Module

The description of the land use management is carried out according to the methodology in the SWAT model (Arnold et al. 1998). The land use management module offers to represent complex crop rotations in J2k-S. The individual field crops are characterized on the basis of management operations like sowing, fertilizing and harvesting. As can be seen in figure 1, the crop rotation relates to an actual plant that in turn is build up of the plant parameters and the individual management options.

<figure>
  <a href="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenmanagementmodul1.jpg' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenmanagementmodul1.jpg' | relative_url }}" alt="Pflanzenmanagementmodul1"></a>
  <figcaption>Figure 1: Flow chart of the land use management module</figcaption>
</figure>

The basic basis objects for the description of the land use management are cultivation (no function yet), fertilization, plant characteristics and the crop rotation. Land management and fertilization as management options have only simple parameters like mixing efficiency, machining depth, amount of fertilizer, ammonium and nitrate. However, the plant object possesses numerous parameters. Thus, the crop rotation is a simple list with the order of the individual crops (see figure 2).

<figure>
  <a href="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenmanagementmodul2.jpg' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenmanagementmodul2.jpg' | relative_url }}" alt="Pflanzenmanagementmodul2"></a>
  <figcaption>Figure 2: Essential components (basic objects)</figcaption>
</figure>

As an explanation in figure 3 a detail of a management parameter file is shown. In the first line a cultivation type can be found. Thereupon, the sowing of the maize that was used in the example follows. Furthermore, three fertilizations with three different fertilizers are carried out. The harvest with the amount of biomass is given. The rest remains on the field and is allocated to the residue pool in the nitrogen module. Finally, cultivation is carried out in this example.

<figure>
  <a href="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenwaschtumsmodul4.jpg' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-models/water-and-nutrient-balance-model-j2000-s/Pflanzenwaschtumsmodul4.jpg' | relative_url }}" alt="Pflanzenwaschtumsmodul4"></a>
  <figcaption>Figure 3: Structure of a management parameter file</figcaption>
</figure>

With the help of this tool, the essential activities of the horticultural management as well as alternatives can be represented flexibly.

## Ground Water Nitrogen Module

The description of the nitrogen's dynamics that occurs in the ground water is carried out according to the ground water dynamics used in J2k. At this, the nitrogen load is – corresponding to the water – allocated to the two ground-water reservoirs RG1 and RG2. The water and matter proportions are generated for both ground-water reservoirs. The output is carried out analogue to the water and the generated proportions. It is possible to set up an origin nitrogen concentration.

Besides, an attenuation factor is implemented that delays the change of the nitrogen proportions in the storage. This factor used for the calibration can be set up for both ground-water reservoirs separately. It represents the mixing and diffusion effects in the aquifer.
