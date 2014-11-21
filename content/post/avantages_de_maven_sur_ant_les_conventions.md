---
title: "Avantages de maven sur ant : les conventions"
description": ""
date: "2006-12-01"
categories: ["articles"]
tags: [ "tools/maven"]
---
On reproche souvent a Maven ses conventions. Moi, je les apprecie, car…

*   lorsque je commence un nouveau projet, c’est moins de questions (avec moi meme ;-)) et de discussions avec les autres developpeurs (chacun ayant ses conventions, habitutes).
*   lorsque je participe a un projet (OpenSource ou non) deja existant, j’ai tout de suite mes reperes :

        *   ou sont les sources, les tests, la doc
    *   comment compiler, packager, lancer les tests, distribuer,…

A partir des conventions de bases, il est possible d’enrichir le projet :

*   ajout de repertoires pour les sources sql (dans mon cas src/main/sql)
*   ajout d’un squelette pour les applications ou service (nt/unix).

          project_home/src/main/app
          |-- run.bat
          |-- run.sh
          |-- *.exe
          |-- lib/
          |    |-- *.dll
          |    |-- *.so
          |-- logs/
               |-- .keep

Il est aussi possible de ne pas respecter les conventions (structures des repertoires), mais cela est deconseille dans la mesure du possible car on perd alors les avantages d’une convention, et certains plugins peuvent ne pas fonctionner.

Et cela n’est pas vraiment possible avec ant, ou tout est du specifique (meme deux projet d’un meme auteur), l’emplacement des sources, le nom de la target qui compile, qui fait le jar,…

Liens :

*   [The Tech Blog of Ken : Moving from Ant to Maven](http://kensoft.blogs.com/the_tech_blog_of_ken/2006/11/moving_ant_to_m.html)