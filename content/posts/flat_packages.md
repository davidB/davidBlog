---
title: "Java/Scala packages without '.'"
description": ""
date: "2010-01-20"
categories: ["articles"]
tags: [ "lang/java", "lang/scala", "convention"]
---
Since some month, I no longer use ‘.’ in package ‘s name but ‘_’.

Pro :

*   less “click” when browsing/navigate into java/scala sources from file system, editor’s “project viewer” or web view of SCM
*   reduce the number of trouble introduce by scala relative import
*   work with IDE (tested with Eclipse and IntelliJ)
*   follow the same directory layout as for .class

Con :

*   against all conventions (java / scala)
*   make using relative imports impossible in scala (IHMO, It’s not a bad idea, relative import doesn’t help code reader who need to know the resolution rules, process them to find from where class come from)
*   scale badly with the number of package, but help to see that your project contains to many package (justify ?)