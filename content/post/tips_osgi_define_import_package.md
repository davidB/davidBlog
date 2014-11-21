---
title: "Eclipse/OSGi : from Require-Bundle to Import-Package"
description": ""
date: "2010-11-26"
categories: ["articles"]
tags: [ "tools/eclipse", "osgi", "tips", "tools/tycho"]
---
Yesterday, I spend too many time to convert Require-Bundle to Import-Package into MANIFEST.MF of eclipse bundles.
For some various cause, I can’t do it with PDE, so I don’t know if there is assistant or not in PDE.
I did it manually (try and catch) : edit, build with tycho, install plugins, restart, try until I’ve got NoClassDefFoundExceptions.

Until I’ve got the idea (late for the last plugin) : using a package analyzer to have the full list of package used by the bundle.
In my case I use JDepend (as I failed to download it, I use a version in my maven local repository) :

    java -cp  ${HOME}/.m2/repository/jdepend/jdepend/2.9.1/jdepend-2.9.1.jar \
      jdepend.textui.JDepend \
      org.scala-ide.sdt.compiler.ext/target/classes
    

At the end of the report there is the list of packages :

    --------------------------------------------------
    - Package Dependency Cycles:
    --------------------------------------------------

    --------------------------------------------------
    - Summary:
    --------------------------------------------------

    Name, Class Count, Abstract Class Count, Ca, Ce, A, I, D, V:

    java.io,0,0,1,0,0,0,1,1
    java.lang,0,0,1,0,0,0,1,1
    scala,0,0,1,0,0,0,1,1
    scala.collection,0,0,1,0,0,0,1,1
    scala.collection.generic,0,0,1,0,0,0,1,1
    scala.collection.immutable,0,0,1,0,0,0,1,1
    scala.collection.mutable,0,0,1,0,0,0,1,1
    scala.collection.script,0,0,1,0,0,0,1,1
    scala.math,0,0,1,0,0,0,1,1
    scala.reflect.generic,0,0,1,0,0,0,1,1
    scala.runtime,0,0,1,0,0,0,1,1
    scala.tools.nsc,0,0,1,0,0,0,1,1
    scala.tools.nsc.ast,0,0,1,0,0,0,1,1
    scala.tools.nsc.dependencies,0,0,1,0,0,0,1,1
    scala.tools.nsc.interactive,180,13,0,22,0,07,1,0,07,1
    scala.tools.nsc.io,0,0,1,0,0,0,1,1
    scala.tools.nsc.reporters,0,0,1,0,0,0,1,1
    scala.tools.nsc.settings,0,0,1,0,0,0,1,1
    scala.tools.nsc.symtab,0,0,1,0,0,0,1,1
    scala.tools.nsc.typechecker,0,0,1,0,0,0,1,1
    scala.tools.nsc.util,0,0,1,0,0,0,1,1
    scala.util,0,0,1,0,0,0,1,1
    scala.util.control,0,0,1,0,0,0,1,1


So I convert 

	Require-Bundle: org.scala-ide.scala.compiler

into 

    Import-Package: scala.tools.nsc,
     scala.tools.nsc.ast,
     scala.tools.nsc.dependencies,
     scala.tools.nsc.io,
     scala.tools.nsc.reporters,
     scala.tools.nsc.settings,
     scala.tools.nsc.symtab,
     scala.tools.nsc.typechecker,
     scala.tools.nsc.util

(Tips to not forgot)