---
title: ""
description": ""
date: "2010-10-12"
categories: ["articles"]
tags: [ "linux" ]
draft: true
---
 

prepare a new local working directory to host gh-pages branch

    # from http://pages.github.com/
    export artifactId=vscaladoc2_genjson
    git clone git@github.com:davidB/${artifactId}.git ${artifactId}-gh-pages
    cd ${artifactId}-gh-pages
    git symbolic-ref HEAD refs/heads/gh-pages
    rm .git/index
    git clean -fdx
    echo "My GitHub Page" > index.html
    git add .
    git commit -a -m ‘reset gh-pages’
    git push origin gh-pages

edit project definition (into master) to generate mvnsite into the new directory : `edit -w ../${artifactId}/pom.xml`

    <properties>
        ...
        <gh-pages-dir>${project.basedir}/../${project.artifactId}-gh-pages</gh-pages-dir>
    </properties>

    <distributionManagement>
      <site>
        <id>gh-pages</id>
        <url>file://${gh-pages-dir}</url>
      </site>
    </distributionManagement>

