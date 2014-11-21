---
title: "Tips: inclure un jar dans un projet maven"
description": ""
date: "2006-12-04"
categories: ["articles"]
tags: [ "tips", "tools/maven"]
---
Plutot que de placer les jar (war,…) dans un sous repertoire lib du projet et de les referencer directement dans le pom.xml (avec le scope system). Je les place dans un sous repertoire `repo-add` (au meme niveau que `src`):

```
    [project]
      |-- pom.xml
      |-- src/
      |    |-- ...
      |-- repo-add/
           |-- install.bat
           |-- install.sh
           |-- foo-1.0.jar
           |-- bar-2.4.jar
           |-- bar-2.4.pom
```

Si je ne veux pas que maven cree des fichiers pom par defaut, je les places aussi dans le repertoire (si je veux ajouter des informations au jar (description, dependances,…)).

Les autres developpeurs utilisent (executent) le script install, qui fait l’installation des artefacts dans leur repository local (tout les utilisateurs de maven en ont un). Ces dependances peuvent ainsi etre referencees dans le pom.xml (du projet) comme les autres dependances. Cela a pour avantages de :

* conserver dans le pom.xml l’information sur le scope reel du jar (compile, test, runtime, provided)
* de maintenir une coherence de classement pour ces dependances entres plusieurs projets
* de pouvoir les supprimer du repertoire repo-add lorsqu’elles deviennent disponible dans un repository public.

```
rem ex de script install.bat
call mvn install:install-file -Dfile=jta.jar -DgroupId=javax.transaction -DartifactId=jta -Dversion=1.0.1B -Dpackaging=jar -DgeneratePom=true
call mvn install:install-file -Dfile=jms-1.0.2b.jar -DgroupId=javax.jms -DartifactId=jms -Dversion=1.0.2b -Dpackaging=jar -DgeneratePom=true

call mvn install:install-file -Dfile=ojdbc14-10.2.0.2.jar -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=10.2.0.2 -Dpackaging=jar
call mvn install:install-file -Dfile=ojdbc14-10.2.0.2.pom -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=10.2.0.2 -Dpackaging=pom

# ex de script install.sh
mvn install:install-file -Dfile=jta.jar -DgroupId=javax.transaction -DartifactId=jta -Dversion=1.0.1B -Dpackaging=jar -DgeneratePom=true
mvn install:install-file -Dfile=jms-1.0.2b.jar -DgroupId=javax.jms -DartifactId=jms -Dversion=1.0.2b -Dpackaging=jar -DgeneratePom=true

mvn install:install-file -Dfile=ojdbc14-10.2.0.2.jar -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=10.2.0.2 -Dpackaging=jar
mvn install:install-file -Dfile=ojdbc14-10.2.0.2.pom -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=10.2.0.2 -Dpackaging=pom
```
