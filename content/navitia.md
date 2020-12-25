+++
category = "tech"
date = 2017-11-14
title = "L’histoire de Navitia"
draft = true
+++

[Navitia](https://navitia.io/) permet de manipuler les horaires de
transports en commun. Parmis la penta-chiée de fonctionnalités, il y a
par exemple le calcul d’itinéraire, des fiches horaires, et tellement
plus.

J’ai pu y contribuer pendant trois ans, mais surtout j’ai pu être témoin
de la mise en place d’un joli éco-système et rencontrer de nombreuses
personnes qui ont rajouté leur pierre à l’édifice de l’information
voyageur. Sans grand coup d’éclat ni grande star, mais patiemment,
petit pas par petit pas.

# 2010 : un nouveau poste

En 2010, je finissais mon doctorat sur les calculs d’itinéraires. Ne
souhaitant pas de continuer dans la recherche pure, je cherchais un
travail.

J’étais tombé sur une vidéo de [Yann Le Tilly](https://twitter.com/transid) où il vantait les mérites de
OpenStreetMap. Cela m’a motivé à faire une candidature spontannée,
malgré leur site web miteux — même pour l’époque — et l’emplacement
douteux de [leurs locaux](https://www.openstreetmap.org/search?query=boulevard%20poniatowski#map=16/48.8297/2.3918).

Dans un costume élimé et chaussé de chaussures prêtées trop étroites
j’ai passé les entretiens entre autres avec [Guillaume Crouigneau](https://twitter.com/gcrouigneau) et [Stephan Simart](https://twitter.com/stifoon) le papa de NAViTiA (ce choix
de majuscule aura été remis en cause) avec qui nous surtout discuté du
programme des *Solidays* qui commençaient le lendemain.

*NAViTiA 1* commençait a accumuler quelques années et était écrit en
Delphi. Mais surtout, il ne tournait que sur Windows et le langage
(pourtant étonnamment plaisant) rendait le recrutement difficile.

Le but était de ré-écrire navitia en C++ et qu’il puisse tourner sous
linux et — qui sait — à terme intégrer OpenStreetMap.

J’ai donc rejoint l’équipe de Stephan aux côtés de Abder, Krishna, Kinou
et Patoche. Un peu plus tard [Vincent Lara](https://twitter.com/VincentLara) nous a rejoint pour intégrer les
nouveaux algorithmes qui [venaient d’être publiés](http://blog.tristramg.eu/petit-historique-du-calcul-ditineraire.html).

L’équipe avait déjà une bonne partie des bonnes habitudes, dont :

-   Une grande batterie de tests d’acceptance ;
-   Une revue de code quasiment systématique (mais en synchrone, le
    relecteur assis à côté du développeur) ;
-   Une grande bienveillance au sein de l’équipe.

# 2012 : données ouvertes

En juin 2012 Transilien décide d’ouvrir ses données théoriques sous
l’influence de Yann qui les avait rejoint entre temps.

Sans réellement apprécier ce moment historique, on m’a demandé à la
dernière seconde si je voulais bien être présent pour répondre aux
questions sur l’API de NAViTiA 1 mise à disposition pour les deux
premier hackathons : [les hackdays en
juin](http://www.sncf.com/ressources/cp_hackdays_-_sncf_transilien_-_01062012.pdf)
et surtout le super [hackathon des
cheminots](http://www.sncf.com/ressources/cp_hackathon_des_cheminots.pdf).

J’y ai connu [Chloé Bonnet](https://twitter.com/chhhloe) et [Kat Borlongan](https://twitter.com/katborlongan) qui créeront plus tard
[Five by Five](https://twitter.com/fivebyfiveio), mais aussi [Jeff Vial](https://twitter.com/Jeff_Vial), [Andrew Byrd](https://twitter.com/globalvoid) ou encore [Pieter Colpaert](https://twitter.com/pietercolpaert), que des personnes
incontournables dans les données transport ouvertes.

J’ai aussi croisé des développeurs. Leurs réponses ont été cinglantes.
Une API en XML documentée dans un document de 100 pages, c’est pas
possible.

# Une API pour développeurs

# Les évolutions suivantes
