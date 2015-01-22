---
layout: post
title: "qtcreator menubar is missing in ubuntu 14.04"
description: ""
category: coding
tags: [qt, ubuntu]
---
{% include JB/setup %}

在ubuntu 14.04下，无论Gnome还是KDE环境，Qtcreator都无法正常显示菜单栏，其实是[Ubuntu的BUG](https://bugs.launchpad.net/ubuntu/+source/appmenu-qt5/+bug/1307619)。


###bug 1307619###

```

1. Open "Qt Creator" at the Gnome3 Desktop
2. Menu bar is missing.

After Deinstall appmenu-qt5 is the Menu bar working again.

ProblemType: Bug
DistroRelease: Ubuntu 14.04
Package: appmenu-qt5 0.3.0+14.04.20140314-0ubuntu1
ProcVersionSignature: Ubuntu 3.13.0-8.28-generic 3.13.2
Uname: Linux 3.13.0-8-generic i686
ApportVersion: 2.14.1-0ubuntu2
Architecture: i386
CurrentDesktop: GNOME
Date: Mon Apr 14 18:52:18 2014
InstallationDate: Installed on 2014-02-14 (58 days ago)
InstallationMedia: Ubuntu 14.04 LTS "Trusty Tahr" - Alpha i386 (20140214)
SourcePackage: appmenu-qt5
UpgradeStatus: No upgrade log present (probably fresh install)

```
移除`appmenu-qt5`就可以正常显示了。
