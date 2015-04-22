---
layout: post
title: "compile qtox on OSX"
date: 2015-03-03 23:49:35 -0500
comments: true
categories: OSX qt c++
---

###Problems when compile qtox on mac
- first is the modification of the qtox.pro file
```
	CONFIG += c++11
	CONFIG += x86_64
	CONFIG -= x86
	contains(JENKINS,YES) {
		INCLUDEPATH += ./libs/include/
	} else {
		INCLUDEPATH += libs/include
	    # add head path
	    INCLUDEPATH += /usr/include
	    INCLUDEPATH += /usr/local/include
	    INCLUDEPATH += /opt/local/include
	}
	macx {
        BUNDLEID = im.tox.qtox
        ICON = img/icons/qtox.icns
        QMAKE_INFO_PLIST = osx/info.plist
        QMAKE_MACOSX_DEPLOYMENT_TARGET = 10.9
        # add libtoxav
        LIBS += -L/usr/local/opt/libtoxcore/lib -ltoxav -ltoxcore
        LIBS += -L/usr/local/opt/libsodium/lib -lsodium
        LIBS += -L/usr/local/opt/libvpx/lib -lvpx
        LIBS += -L/usr/local/lib -lopus
        LIBS += -L/usr/local/lib -lopencv_core -lopencv_highgui
        #LIBS += -L/opt/local/lib -lopencv_core -lopencv_highgui
        LIBS += -L$$PWD/libs/lib/ -framework OpenAL -mmacosx-version-min=10.9
        #LIBS += -L$$PWD/libs/lib/ -ltoxcore -ltoxav -ltoxencryptsave -ltoxdns -lsodium -lvpx -lopus -framework OpenAL -lopencv_core -lopencv_highgui -mmacosx-version-min=10.7
        contains(DEFINES, QTOX_PLATFORM_EXT) { LIBS += -framework IOKit -framework CoreFoundation }
        contains(DEFINES, QTOX_FILTER_AUDIO) { LIBS += -lfilteraudio }
```

<!--more-->
- 1.-ltoxcore can not found
	- install the toxcore library 
		- and remember to add the library path

- 2.can not find -lopus
	- install the libogg first and then install the opus library

- 3. “Project ERROR: Could not resolve SDK path for ‘macosx10.8′”.
	- `cd /Users/Mark/Qt/5.3/clang_64/mkspecs/`
		- modify `!host_build:QMAKE_MAC_SDK = macosx10.9`

- 4."Undefined symbols for architecture x86_64"
	- **not solved**
		- one way on the Internet(did not solve)
			- change `../Qt5.4.0/5.4.0-rc1/clang_64/mkspecs/macx-clang/qmake.conf`
				- from `QMAKE_MACOSX_DEPLOYMENT_TARGET = 10.6`
				- into `QMAKE_MACOSX_DEPLOYMENT_TARGET = 10.9`
					- and remember to clean the project before rebuild

- 5.'#include <>' and '#include ""'
	- '#include <>'
		- find the header in particular path
			- /usr/include
			- for exmaple: /usr/include/stdio.h
	- '#include ""'
		- find the header in absolute path



