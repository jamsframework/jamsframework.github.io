---
layout: doc
title: Starting JAMS
section: JAMS Setup & Configuration
section_url: /documentation/#jams-setup
---

## Start Options

JAMS provides two primary graphical interfaces:

1. **JAMS Launcher**: Enables loading, running, and saving models, editing parameters, and analyzing results.
2. **JAMS Builder**: Permits modifying JAMS model structure (components, spatio-temporal iteration, control flow) with launcher functionality.

A command line interface also supports loading and running JAMS models.

Access these through starter scripts or executables in the JAMS installation root directory:

| Interface | Windows | Linux / OS X |
|-----------|---------|--------------|
| JAMS Launcher | jams.exe; jams.bat | jams.sh; jams.command |
| JAMS Builder | juice.exe; juice.bat | juice.sh; juice.command |
| Command line without GUI | `java <JAVA_OPTIONS> -splash: -jar jams-starter.jar -n -m <MODEL_FILE>` | |

### Setting Available Memory

**For starter scripts**, edit and update the **-Xms** and **-Xmx** options:

```
java -Xms100m -Xmx500m -jar jams-starter.jar
```

Use "m" for MB and "g" for GB units.

**For executables**, edit *jams.l4j.ini* or *juice.l4j.ini* files:

```
-Xms100m
-Xmx500m
```

**From command line**:

```
java -Xms100m -Xmx500m -splash: -jar jams-starter.jar -n -m <MODEL_FILE>
```

### Setting Location of Platform-Dependent Libraries

Use the **-Djava.library.path** option:

**For starter scripts**:

```
java -Djava.library.path=bin/linux64 -jar jams-starter.jar
```

**For executables**, edit *jams.l4j.ini* or *juice.l4j.ini*:

```
-Djava.library.path=bin/linux64
```

## JAMS Command Line Arguments

| Short | Long | Function |
|-------|------|----------|
| -h | --help | Print help |
| -c | --config \<config file name\> | Load configuration from file |
| -m | --model \<model definition file name\> | Load model from file |
| -s | --snapshot \<snapshot file name\> | Load model from snapshot file |
| -n | --nogui | Suppress all graphical output |
| -p | --parametervalue \<list of parameter values\> | Provide parameter values divided by semicolons |
| -j | --parameterfile \<parameter file name\> | Load parameters from file |

### JAMS Without Graphical Output

Using starter scripts:

```
./jams.sh -n -m data/j2k_gehlberg/j2k_gehlberg.jam
```

Or starting Java directly:

```
java -splash: -jar c:/jams/jams-starter.jar -n -m c:/jams/data/j2k_gehlberg/j2k_gehlberg.jam
```

### Transferring Model Parameters during JAMS Start

The **-p/--parametervalue** argument accepts semicolon-separated parameter values assigned via positioning. Wildcards in the model configuration file use the form "%x%", where x is a consecutive number beginning at 0.

Example:

```
./jams.sh -n -m data/j2k_gehlberg/j2k_gehlberg.jam -p "0.1;7;1996-11-01 7:30 2000-10-31 7:30 6 1"
```

Here, "%0%" gets replaced by "0.1", "%1%" by "7", and "%2%" by the date/time string. This enables batch processing of simulation runs.

Alternatively, use **-j/--parameterfile** to load parameters from a file:

```
./jams.sh -n -m data/j2k_gehlberg/j2k_gehlberg.jam -j model.jmp
```

Parameter files contain key/value pairs ("parametername=parametervalue"), one per line, with ".jmp" file extension. These can be exported from JAMS Launcher or Builder and are found in model workspace output folders after execution.
