---
layout: doc
title: Parameter Files with Type Information
section: JAMS Features
section_url: /documentation/#jams-features
---

Parameter files are typically read in JAMS using the `StandardEntityReader` component from the J2000 repository. This component interprets data as Doubles or String values only. While this works for most numeric data, problems arise when components expect different data types, such as integers.

## The Problem

Consider a scenario where sub-catchments need to link to specific runoff measurements. A parameter file might look like this:

```
#gauged subcatchments.par
ID gauging station    subBasinIDs             obsQcolumn
...
0  Arnstadt           [91,92,93,94,98,99,100] 1
1  Gehlberg           [98,99,100]             2
2  Graefinau Angstedt [64,65,66]              3
```

Each sub-catchment has an ID, gauging station name, sub-catchment IDs, and a column reference. The `StandardEntityReader` reads this file into an `EntityCollection` called "gauges." A `SpatialContext` can then iterate over gauges to compute simulated stream-flow and efficiency measures. This can be done with the following sub-model:

<figure>
  <a href="{{ '/assets/img/documentation/jams-features/parameter-files-with-type-information/blog1_01.jpg' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-features/parameter-files-with-type-information/blog1_01.jpg' | relative_url }}" alt="GaugeContext"></a>
  <figcaption>Figure 1 – GaugeContext</figcaption>
</figure>

The `GaugeContext` iterates through sub-catchments, with a `SubBasinFlowAggregator` summing runoff from multiple sub-catchments into a total value stored as `totQ`.

<figure>
  <a href="{{ '/assets/img/documentation/jams-features/parameter-files-with-type-information/blog1_02.png' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-features/parameter-files-with-type-information/blog1_02.png' | relative_url }}" alt="SubbasinFlowAggregator"></a>
  <figcaption>Figure 2 – SubbasinFlowAggregator</figcaption>
</figure>

The `obsRunoff` component (`StandardTSDataProvider`) selects a specific index from a `DoubleArray` using the column ID to retrieve observed runoff data (`obsQ`).

<figure>
  <a href="{{ '/assets/img/documentation/jams-features/parameter-files-with-type-information/blog1_03.png' | relative_url }}"><img src="{{ '/assets/img/documentation/jams-features/parameter-files-with-type-information/blog1_03.png' | relative_url }}" alt="StandardTSDataProvider"></a>
  <figcaption>Figure 3 – StandardTSDataProvider</figcaption>
</figure>

**The core issue:** `StandardTSDataProvider` expects an integer, but the parameter file provides a double value.

## Possible Solutions

1. Create a new component converting double to integer (useful generally, but enlarges the model)
2. Write a specialized `StandardTSDataProviderDoubleVersion` (works, but creates repository bloat)

## The Solution: Type Support

Since version 3.0_b12, users can add a `#TYPED` comment to parameter files. This tells the `EntityReader` to expect an additional header line defining data types.

Supported types include: `Double`, `DoubleArray`, `Float`, `FloatArray`, `Integer`, `IntegerArray`, `Long`, `LongArray`, `String`, `Calendar`, `TimeInterval`, `Boolean`, and `BooleanArray`.

The updated parameter file:

```
#gauged subcatchments.par
#TYPED
ID     gauging station    subBasinIDs             obsQcolumn
Double String             DoubleArray             Integer
...
0      Arnstadt           [91,92,93,94,98,99,100] 1
1      Gehlberg           [98,99,100]             2
2      Graefinau Angstedt [64,65,66]              3
```
