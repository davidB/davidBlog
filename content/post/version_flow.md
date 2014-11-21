---
title: "My versionning flow"
description": ""
date: "2011-05-29"
categories: ["articles"]
tags: [ "misc"]
---
Manual tagging

    VERSION_CURRENT=1.1.0
    VERSION_NEXT=1.2.0
    git checkout wip
    git tag v${VERSION_CURRENT}
    git checkout milestones
    git merge --no-ff v${VERSION_CURRENT}
    # build
    git push origin milestones
    git checkout wip
    # change version number
    git commit -avm "init version ${VERSION_NEXT}"
    git ush origin wip

In the specific case of [ScalaIDE](http://scala-ide.org/) I use the following information to manage the 1.x.y versions.

    wip => wip_exp_backport
    build =
      cd org.scala-ide.build
      ./build-ide-local-2.8.1.final.sh
    change version number =
      cd org.scala-ide.build
      ./set_version.sh ${VERSION_NEXT}-SNAPSHOT
      grep -r ${VERSION_CURRENT} ../**/pom.xml
      grep -r ${VERSION_CURRENT} ../**/MANIFEST.MF
      # build and fix any issue related to version modification
