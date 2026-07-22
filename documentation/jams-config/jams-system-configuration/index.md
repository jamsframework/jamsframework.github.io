---
layout: doc
title: JAMS System Configuration
section: JAMS Setup & Configuration
section_url: /documentation/#jams-setup
---

The system configuration file (with *.jap extension) contains general execution information for JAMS, including:

- **debug=\<0..3\>**: Output verbosity level (0=none, 3=maximum)
- **verbose=\<0,1\>**: Flag for command line info and error notices
- **infolog=\<filename\>**: Info log file name (blank = no file)
- **errorlog=\<filename\>**: Error log file name (blank = no file)
- **libs=\<dir1|jar1;…;dirN|jarN\>**: Semicolon-separated list of directories and libraries available at runtime
- **windowenable=\<0,1\>**: Flag for model window display
- **windowwidth=\<size in pixels\>**: Model window width
- **windowheight=\<size in pixels\>**: Model window height
- **windowontop=\<0,1\>**: Flag for keeping model window in foreground
- **guiconfig=\<0,1\>**: Flag for JAMS Launcher display
- **guiconfigwidth=\<size in pixels\>**: JAMS Launcher window width
- **guiconfigheight=\<size in pixels\>**: JAMS Launcher window height
- **errorlog=\<0,1\>**: Flag for error dialog box display

Most parameters can be edited through the "Extras→Edit Options" menu in either the JAMS Launcher or model editor, where configuration files can also be saved or loaded.
