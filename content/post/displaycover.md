---
title: "displayCover"
description: ""
date: "2007-08-30"
categories: ["articles"]
tags: [ "project"]
---
“displayCover.py” est un petit script  qui permet d’associer une image  automatiquement a un dossier (et ses sous-dossiers).

Suite aux billets [Apercu du dossier dans Nautilus](http://www.greguti.com/petitlinux/index.php?entry=entry070828-172847) et [Aperçu du dossier dans Konqueror](http://blog.bmaron.net/index.php?post/2007/08/28/Apercu-du-dossier-dans-Konqueror), j’ai fait un petit script “displayCover.py” qui permet d’associer une image  automatiquement a un dossier (et ses sous-dossiers).

Commentaires, suggestions, patch sont les bienvenues.

    Usage: displayCover.py [options] dir

    Options:
      --version             show program's version number and exit
      -h, --help            show this help message and exit
      -i ICONNAME, --icon=ICONNAME   filename of icon image (default: cover.png)
      -f, --freedesktop     generate freedesktop, KDE .directory file (default: false)
      -n, --nautilus        generate nautilus metafiles (default: false)
      -r, --replaceAlways   always replace/update files (=&gt; no prompt) (default: false)
      -k, --keepFile        never replace files (=&gt; no prompt) (default: false)
      -q, --quiet           don't print status messages to stdout
      -d, --debug           print debug messages to stdout
    `</pre>

    La version 0.3 (2007-08-30) demande par defaut s’il faut ou non remplacer les fichiers existants, mais possede les options ‘-r’ pour remplacer automatiquement sans confirmation et ‘-k’ pour ne jamais remplacer.

    ## Instructions

    <pre>`# telecharger le script
    wget http://dwayneb.free.fr/download/displayCover.py
    # le rendre executable
    chmod +x displayCover.py
    # afficher l'aide
    ./displayCover.py -h
    # generer les apercus pour freedesktop (inclue KDE) et nautilus
    ./displayCover.py --freedesktop --nautilus mon_dossier
    # restart nautilus
    killall nautilus

## ATTENTION

*   displayCover remplace les fichiers .directory existants !!
*   displayCover met a jour les fichiers de propriete de nautilus existants !!
*   je n’ai pas KDE, donc je n’ai pas fait de test avec (un retour SVP)

## Commentaires (Blog precedent)

* * *

From : Moe
On Monday 10 September 2007, 04:07 AM

Merci beaucoup pour ce script, c’est génial.

Je croyais être tombé sur un bug alors que c’était Nautilus qui me jouait un tour : je croyais que –icon=”.cover.jpg” ne fonctionnait alors que c’était Nautilus qui ne mettait pas à jour l’affichage. Il fallait “simplement” redémarrer Nautilus après avoir changé le nom des miniatures.

La taille des images jpg est très inférieure à celle des images png mais on perd les effets …

Voici la commande que j’utilise : ./displayCover.py -r –icon=”.cover.jpg” –nautilus –select=first .

* * *

From : Moe
On Monday 10 September 2007, 04:12 AM

Oups, j’ai oublié une question : est-il possible d’empêcher le script d’agir récursivement sur tous les sous-répertoires ? On pourrait définir max-depth= avec la valeur 0 pour ne créer des miniatures que des sous-répertoires présents dans le dossier courant.

set offline - edit - delete

* * *

From : David Bernard
On Monday 10 September 2007, 09:28 AM

Merci pour le retour. Je vais voir comment ajouter la possibilite de ne faire qu’un niveau de repertoire (ou mieux controler la navigation dans les repertoires).

* * *

From : toto
On Monday 15 October 2007, 11:33 AM

Le top serait d’ajouter ce patch à Gnome Nautilus…

* * *

From : David Bernard
On Tuesday 16 October 2007, 09:38 AM
Email :
Site :
@IP : 82.240.145.40

@Toto

Je n’ai pas compris ta derniere remarque. Il ne s’agit pas d’un patch. Que suggeres-tu exactement ?

* * *

From : Panda
On Thursday 17 April 2008, 02:10 PM

Salut, merci pour ton script, mais comment revenir en arrière ?

* * *

From : shenga
On Monday 19 May 2008, 08:54 PM

Merci beaucoup pour ce script ! Je n’ai pour l’instant relevé aucun bug .

* * *

From : Esppat
On Friday 18 July 2008, 09:23 PM

J’ai l’erreur suivante après quelques instants :

IOError: [Errno 36] File name too long: ‘… (je vous passe le nom en question, effectivement très long)’.

Je reconnais que l’arborescence de mes fichiers est conséquentes, mais elle est importante pour moi (pour nous …).

Une idée pour gérer ça ?

Je profite de ce post pour indiquer une modif que j’ai faite dans la fonction defineCover :

def defineCover(arg, dirname, names) :
if dirname.find(“/.”,0) &gt;= 0 :
return
logging.info(“analyse %s”, dirname)

J’ai ajouté la deuxième et troisième ligne pour éviter de traverser les répertoires cachés (ceux qui commencent par le caractère point ‘.’). Cette modification n’a pas d’incidence sur le bug mentionné.

Merci !

* * *

From : poncin
On Tuesday 7 October 2008, 10:55 AM

Salut,
Il n’est jamais trop tard…
MERCI pour ton script qui fonctionne nikel.
J’ai juste du remplacer Cover par folder

* * *

From : roumano
On Wednesday 1 July 2009, 01:53 PM

Bonjour,

Sympa ton script !

Quelques détails :

*   J’ai eu cette erreur (vu que sur un seul répertoire :
2009-07-01 13:43:00,115 INFO create file : /home/roums/.nautilus/metafiles/file:%2F%2F%2Fhome%2FMp3%2F0%2520Roots%2FBen%2520Harper.xml
Traceback (most recent call last):
File “/usr/lib/python2.6/logging/**init**.py”, line 773, in emit
stream.write(fs % msg.encode(“UTF-8”))
UnicodeDecodeError: ‘ascii’ codec can’t decode byte 0xc3 in position 83: ordinal not in range(128)
*   Si je ne précise pas l’option –select=’first’ ou last, alors le script ne prend jamais l’un des fichier images de mes répertoires.
*   Cette option n’est pas affichier dans ./displayCover.py -h
*   ./displayCover.py –version renvoi version : 0.4.2
alors que dans le fichier : CHANGELOG 0.5 : …
*   Au début, j’avait pas le programme convert alors que ton script tente de l’utiliser sans vérification ni pré-requis…

* * *

From : dwayne
On Wednesday 29 July 2009, 03:21 PM

Merci, pour les retrours. desole pour le delai. Je ne regarde pas souvent mon feed RSS on mon blog (il faudrait que cela change ;) ).

pour les bugs indiques, je vais voir si je peux les reproduire et les corriger pendant les vacances.

* * *

From : Ptigrouick
On Saturday 1 August 2009, 01:23 PM

Bonjour,

Je viens tout juste de découvrir ton script qui à l’air sympa. Je serai prêt à l’adopter, mais je me pose une dernière question. Les chemins des images étant stockées en absolus depuis la racine, que se passe-t-il si on déplace l’ensemble de la collection musicale. Faut-il réexécuter le script pour chacun des dossiers ? Mon souci c’est que les pochettes de mes albums ont toutes un nom différent (elles contiennent le nom de l’album). Impossible donc pour moi de renommer les pochettes récursivement en utilisant ta commande dans un script…

* * *

From : Roumano
On Sunday 8 November 2009, 03:13 PM

Attention, ce script ne fonctionne plus avec gnome sur ubuntu 9.10 (gnome 2.28), ainsi que, surement, toutes les nouvelles distribution utilisant cette version de gnome,

la raison : c’est gvfs qui gére les metadata maintenant :
ubuntuforums.org/archive/…
Et ici des infos pour modifier le script afin de le faire fonctionner avec cette nouvelle version :
ubuntuforums.org/showthre…

os.system(‘gvfs-set-attribute “‘+p+’” metadata::custom-icon “.folder_bg.thumbnail”’)

Préviens-moi si tu met a jour ton script, je voudrait bien pouvoir l’utiliser.
