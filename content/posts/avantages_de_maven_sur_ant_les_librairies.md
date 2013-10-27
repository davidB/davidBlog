---
title: "Avantages de maven sur ant : les dependances"
description": ""
date: "2006-12-02"
categories: ["articles"]
tags: [ "tools/maven"]
---
Les dependances sont les objets jar, war, ejb,… necessaires a un projet pour etre compile, teste, execute,…

J’aime (en tant qu’utilisateur d’un projet):

*   savoir qu’elle est la version de chaque dependance d’un framework ou d’une librairie que j’utilise
*   savoir ou servent les dependances (compilation, tests, execution, pour les outils de build,… optionnel)

J’aime (en tant que developpeur d’un projet):

*   savoir qu’elle est la version de chaque dependence d’un projet.
*   separer les dependances suivant l’usage qui en est fait (compilation, execution, pour les outils de build,…)
*   la resolution des dependances indirectes (les dependances des dependances), ce qui evite d’aller a la “peche” comme souvent le cas lors de l’inclusion d’une librairie dans un projet ant (avec parfois des erreurs a l’execution). Cela peut alleger un projet car si une dependances indirecte n’est plus utilisees par une nouvelle version d’une dependance directe, alors elle sera automatiquement supprimees de la liste de toutes les dependances.

Ces informations ou fonctions sont rarement presentent dans les projets base sur ant (et l’utilisation d’Ivy ne fait pas tout).

## Dependances hors projet

Il est reproche par les utilisateurs de ant, que les projets maven ne contiennent pas leurs librairies (j’avais le meme point de vue). En quoi cela est-il genant ?

Personnellement, j’utilise les jar des repositories public quand ils sont disponibles. Pour les indisponibles :

*   Si leur license ne permet la distribution sur un repository “public” (eg: driver jdbc Oracle, jta,…), alors je les [inclue dans le projet](/tips_inclure_un_jar_dans_un_projet_maven).
*   Si leur license permet la distribution, mais qu’il n’existe pas ou pas dans la version souhaitee, alors soit je l’inclue dans mon projet, soit je le publie dans un repository accessible  par les autres developpeurs/contributeurs et les utilisateurs (si mon projet ne les inclue pas la version distribue (ex: une librairie)). Dans le cas d’une version manquante, je peux contacte le mainteneur pour faire la mise a jour.

## Projet ant sans dependances incluses

Certains projets ant n’incluent pas leur dependances, mais font references a des jars externes:

*   par des chemins absolues :-/, ou relatif, (et c’est de nouveau la peche, surtout si les jars ne sont pas liste mais reference *.jar dans le build.xml)
*   qui sont dans un autre projet, ou qui sont generes par un autre projet . Et la cela devient infernal pour le contributeur qui doit aussi installer/comprendre le(s) autre(s) projet(s), et les placer dans les bons repertoires. Maven peut avoir le meme probleme avec les projets avec sous modules, mais cela reste limite, documente et suit une convention.

En gros cela demande trop de travail pour le contributeur, qui va souvent abandonner, “forker”, juste prendre ce qui l’interresse,…