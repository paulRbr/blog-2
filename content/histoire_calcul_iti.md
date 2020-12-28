+++
category = "tech"
date = 2013-07-07
title = "Petit historique du calcul d’itinéraire"
+++

# Introduction

Plus formellement pour parler de calcul d’itinéraire, on parlerait du
« problème du plus court chemin dans un graphe ». La finalité reste la
même : qu’est-ce qu’il y a de plus court pour aller de A vers B.

Les calculs d’itinéraires ont ceci de sympa que l’application finale
parle à n’importe qui :

-   l’utilisateur final qui utilise un GPS
-   l’étudiant en informatique a appris à un moment les algorithmes de
    base
-   le sujet reste encore assez pointu algorithmiquement mais explicable
    à celui qui s’y intéresse le temps de quelques pintes

Ce que je trouve intéressant, c’est l’évolution dans le temps de ces
algorithmes. Je m’excuse pour les détails techniques ponctuels.

# 1959 : Dijkstra

[Edgard Dijkstra](https://en.wikipedia.org/wiki/Edsger_W._Dijkstra) est
néerlandais. Le « ij » de son nom se prononce donc « ail » comme celui
que vous utilisez pour éloigner les vampires.

C’est un des grands noms de l’informatique, connu pour son écriture
manuscrite, ses citations telles que :

-   `Simplicity is prerequisite for reliability`
-   `The question of whether Machines Can Think... is about as relevant as the question of whether Submarines Can Swim`
-   `Object-oriented programming is an exceptionally bad idea which could only have originated in California`

C’est l’auteur de --- attention, scoop --- *l’algorithme de Dijkstra*
publié en 1959. Il a été décrit dans un article qui fait seulement [deux
pages](http://www-m3.ma.tum.de/foswiki/pub/MN0506/WebHome/dijkstra.pdf)
mais dont le nom restera comme le fondamental du calcul d’itinéraire.

Cependant, l’algorithme qu’on apprend à l’école n’est pas celui qui est
publié par Dijkstra. Il a en effet une complexité de O(n²) alors qu’on
nous enseigne que la complexité de l’algorithme est en O(n·log(n)).

Il faut attendre 28 ans pour y arriver.

# 1987 : Tarjan

Le point faible de l’algorithme de Dijkstra est sa queue de priorité qui
remonte le prochain nœud du réseau à visiter. La publication par Tarjan
(une autre référence dans le monde des Graphes) d’un [article en
1987](http://www.cs.princeton.edu/courses/archive/fall03/cs528/handouts/fibonacci%20heaps.pdf)
nous amène à la version « moderne » de l’algorithme de Dijkstra.

Différentes variantes ont été testées pour accélérer l’algorithme avec
des succès moyens, comme le A*, les recherches bi-directionnelles, des
sacrifices à l’optimum, ou encore une combinaison de tout ça.

Sur un ordinateur récent, calculer un itinéraire en France prend environ
une seconde. Dans les années 90 c’était donc encore bien trop lent. Il
fallait donc trouver comment accélérer le calcul.

Il faut attendre 18 ans pour y arriver.

# 2005 : challenge Dimacs and rise of the KIT

Le thème du [9ème Challenge
Dimacs](http://www.dis.uniroma1.it/challenge9/format.shtml) était le
calcul d’itinéraire. À cette occasion le [réseau routier des
États-Unis](http://www.dis.uniroma1.it/challenge9/download.shtml) a été
diffusé.

De très nombreuses publications ont pulvérisé tous les records. On peut
désormais calculer un itinéraire entre deux points de la planète en
moins d’une milliseconde (soit des *milliers* de fois plus rapide que
l’algorithme de Dijkstra).

Un grand nombre de publications viennent du [Karlsruhe Institute of
Technology](http://i11www.iti.uni-karlsruhe.de/en/projects/route_planning/index).

Les membres de cette équipe ont proposé de nombreux algorithmes, mais
ont également testé presque toutes les combinaisons possibles entre ces
algorithmes.

Ça devenait la foire et on ne savait plus trop où donner de la tête.

# 2008 : la consolidation avec les Contraction Hierarchies

Après cette phase d’ébullition et de créativité, on a pu tirer la
substance essentielle pour arriver à l’algorithme qui deviendra
probablement la nouvelle référence : les *contraction hierarchies*.

Il a été présenté dans un thèse de master (du coup j’ai un peu honte de
ma thèse de doctorat moi...) par
[Geisberger](http://algo2.iti.kit.edu/documents/routeplanning/geisberger_dipl.pdf).

Il n’y a pas vraiment de nouveautés, juste une suppression de tout le
superflu rendant d’autres algorithmes trop compliqués pour ne garder que
le cœur qui fonctionne bien.

J’invite ceux qui s’intéressent à l’algorithmie à lire l’algorithme et
surtout sa démonstration très agréable. À la première lecture on se dit
que ça ne peut pas marcher et il faut vraiment dérouler la démonstration
pour s’en convaincre.

C’est cet algorithme qui est utilisé dans
[OSRM](http://map.project-osrm.org/), un calculateur Libre qui se base
sur les données [OpenStreetMap](http://www.openstreetmap.org).

# 2009 : les transports en communs, enfant pauvre de la recherche

On sait donc enfin calculer efficacement un itinéraire sur un réseau
routier. Mais qu’en est-il en transports en communs ? C’est vraiment pas
la joie.

Les performances sont décevantes, et les tentatives d’appliquer les
succès sur les réseaux routiers ont échoué.

Dans l’article [Car or Public Transport—Two
Worlds](http://link.springer.com/chapter/10.1007/978-3-642-03456-5_24)
H. Bast souligne les différences qui existent entre les deux mondes et
qu’il n’est pas pertinent d’essayer de se rapprocher.

# 2010 : transfer patterns, enfin la performance

C’était l’été, je venais d’envoyer mon manuscrit de thèse aux
rapporteurs. Par acquis de conscience j’ai lu le [nouvel article de H.
Bast](http://ad.informatik.uni-freiburg.de/files/transferpatterns.pdf).

Pour la première fois, on arrivait à calculer des itinéraires en
quelques millisecondes en utilisant les transports d’une grande ville
(comme New-York).

À y regarder de plus près, c’était quand même tricher : en utilisant la
puissance de milliers d’ordinateurs dont dispose Google, un pré-calcul
massif est la clef de ces performances.

Plus que deux ans à attendre avant d’avoir un algorithme performant

2012 : Raptor de Delling
========================

Daniel Delling affectionne les noms qui ont la classe (un précédent
algorithme s’appelait Sharc). Il a donc proposé
[Raptor](http://research.microsoft.com/apps/pubs/default.aspx?id=156567).

L’approche proposée ne nécessite pas de pré-calcul et a pourtant de
meilleures performances que les transfer patterns.

Hourray ! Les voitures n’ont plus le monopole des algorithmes efficaces
! Raptor a en plus l’avantage d’être plutôt simple et d’avoir des
propriétés intéressantes.

Les 6 ans d’écarts entre le premier algorithme routier haute
performances avec le premier algorithme haute performances pour
transports en commun s’explique probablement tout simplement par
l’absence de données de transports en commun utilisables par la
recherche.

C’est le mouvement open data appliqué aux transports qui a permis ces
progrès scientifiques.

2013 : Connection Scan Algorithm
================================

Le dernier pour la route ! Dans un article très modestement nommé
[Intriguingly Simple and Fast Transit
Routing](http://link.springer.com/chapter/10.1007%2F978-3-642-38527-8_6)
les auteurs présentent le *connection scan algorithm*. Il est légèrement
plus performant que Raptor, mais il est considérablement plus simple.

À la lecture de l’article, puis à nouveau à l’implémentation, on est
étonné de voir à quel point c’est encore plus bête qu’un pigeon, mais ça
marche.

On fait un voyage de 54 ans dans les calculs d’itinéraires pour arriver
sur un algorithme qui aurait pu être développé en même temps que celui
de Dijkstra.

Du coup on va finir par une dernière citation de Dijkstra qui me semble
tout à propos :

> Simplicity is a great virtue but it requires hard work to achieve it and education to appreciate it. And to make matters worse: complexity sells better
