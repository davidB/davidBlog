---
title: "My Eclipse Setup"
description": ""
date: "2010-06-13"
categories: ["articles"]
tags: [ "tools/eclipse", "lang/java", "lang/scala" ]
---
Since 2000, I’m a eclipse user, mainly for java coding. This article is a live article ( == I’ll update it) I’ll use to list and to memorize my eclipse setup (plugins, ini, preferences,…).

Since 2010 (since I stop coding in scala 2.7.x), I use it for my Scala dev. Previously, I used [JEdit](http://jedit.org/), emacs, netbeans - 6 month min each and 1 month for IntelliJ.

As text editor I also used : [JEdit](http://jedit.org/) (this article is writing with it), [SciTE](http://www.scintilla.org/SciTE.html) and [gnu nano](http://www.nano-editor.org/)

Eclipse version : **3.5.2** for Linux 64bit + JDK 1.6.0_20 64 bit (Sun)

## Ini

My `eclispe.ini` file.

    -startup
    plugins/org.eclipse.equinox.launcher_1.0.201.R35x_v20090715.jar
    --launcher.library
    plugins/org.eclipse.equinox.launcher.gtk.linux.x86_64_1.0.200.v20090519
    -showsplash
    org.eclipse.platform
    --launcher.XXMaxPermSize
    384m
    -vmargs
    -server
    -XX:PermSize=256m
    -XX:MaxPermSize=384m
    -Xss2m
    -Xms512m
    -Xmx2g
    -XX:MaxGCPauseMillis=10
    -XX:+ScavengeBeforeFullGC
    -XX:-UseParallelOldGC
    -XX:+HeapDumpOnOutOfMemoryError
    -XX:+CMSClassUnloadingEnabled
    -Duser.name=david.bernard
    -Dosgi.requireJavaVersion=1.6
    -Declipse.p2.unsignedPolicy=allow
    #-Xms256m
    #-Xmx1024m
    #-Xss1m
    #-server
    #-XX:+UseConcMarkSweepGC

## References :

*   [Optimizing Eclipse performances](http://blog.normation.com/2010/05/24/optimizing-eclipse-performances/) from [Normation](http://blog.normation.com/).
*   [What are the best JVM settings for Eclipse?](http://stackoverflow.com/questions/142357/what-are-the-best-jvm-settings-for-eclipse) from [Stack Overflow forum](http://stackoverflow.com/)
*   [ScalaIDE Setup](https://www.assembla.com/wiki/show/scala-ide/Setup)

I use different memory setup, because I’ve ‘only’ 4Go Ram and a 64bit machine, and when start launch eclipse to test/debug my eclipse plugin. With higher values for -Xms, I got lot of error about memory.

## Plugins

*   UI
    *   **[Mousefeed](http://www.mousefeed.com/)** (1.0.0) : Key promoter (Helps to remember keyboard shortcuts)
        *   provider : Heavy Lifting software
        *   update-site : http://update.mousefeed.com
*   Jvm (.java, .scala, .class) tools
    *   **[M2Eclipse](http://m2eclipse.sonatype.org/)** (0.12.0) :  maven integration into eclipse
        *   provider : [Sonatype Inc](http://sonatype.org/)
        *   update-site : http://m2eclipse.sonatype.org/sites/m2e
    *   **[M2Eclipse-scala](http://gitup.com/sonatype/m2eclipse-scala)** (0.2.3) :  m2eclipse + scala
        *   provider : [Sonatype Inc](http://sonatype.org/) + David Bernard (myself)
        *   update-site : http://alchim31.free.fr/m2e-scala/update-site/
    *   **[Scala Eclipse Plugin](http://scala-ide.org/)** (wip_exp_backport for scala 2.8.1) : an experimental branch of the plugin (own by myself)
        *   provider : scala-ide.org
        *   update-site : http://download.scala-ide.org/nightly-update-wip-exp-backport-2.8.1.final
    *   **[Findbugs](http://findbugs.sourceforge.net/)** (1.3.9) : static .class (from java and may be scala) code analyzer
        *   provider :
        *   update-site : http://findbugs.cs.umd.edu/eclipse
    *   **[UCDetector](http://www.ucdetector.org/)** (1.4.0) : Unnecessary Code Detector finds unnecessary (dead) public java code.
        *   provider : Jörg Spieler
        *   update-site : http://ucdetector.sourceforge.net/update
    *   **[PMD For Eclipse](http://pmd.sourceforge.net/integrations.html#eclipse)** (3.2.6) : static java code analyzer ( include CPD for copy/paste detection)
        *   provider :
        *   update-site : http://pmd.sf.net/eclipse
*   Text Editor
    *   **[AnyEditTools](http://andrei.gmxhome.de/anyedit/index.html)** (2.3.1) : Adds useful context menu actions to text files and editors
        *   provider : [Andrei Loskutov](http://andrei.gmxhome.de/)
        *   update-site : http://andrei.gmxhome.de/eclipse/
*   Misc
    *   **[QuickREx](http://www.bastian-bergerhoff.com/eclipse/features/web/QuickREx/toc.html)** : to test regular expression
        *   provider : Bastian Bergerhoff
        *   update-site : http://www.bastian-bergerhoff.com/eclipse/features
*   Console Enhancement
    *   **[Grep console](http://marian.musgit.com/projects_grepconsole.php)** : to have color in Console output (log, external builder,…)
        *   provider : Marian Schedenig
        *   update-site : http://eclipse.musgit.com/
    *   **[Wicked Shell](http://www.wickedshell.net/)** : direct access to your system’s shell in eclipse
        *   provider :*   update-site :  http://www.wickedshell.net/updatesite
…