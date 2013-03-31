Paris en 1734
#############

:date: 2012-1-7 23:20
:tags: cartographie, paris
:category: carto
:author: Tristram Gräbener


Hoplà ! Ce coup-ci c’est pas du tout polémique. Just un mini-tuto sur comment superposer une vieille carte sur une toute nouvelle.

Voici le résultat : http://vrac.tristramg.eu/Turgot2/openlayers.html

Lisez la suite si vous savoir comment faire.

Nous allons utiliser le Plan Turgot de 1734. C’est à peu près la première carte de Paris qui soit suffisemment fiable.
Plus d'information sur ... Wikipedia *of course* : http://fr.wikipedia.org/wiki/Plan_de_Turgot

Je me suis pas mal basé sur ce billet : http://shawnsbits.com/blog/2010/12/23/mapkit-overlays-session-1-overlay-map/

Correspondance Pixels – coordonnées
***********************************

On commence par télécharger la carte. C’est un JPEG de 6 552 × 5 101 pixel. Il faut donc commencer par géo-tagger la carte. Pour cela, il faut repérer des points en pixels et trouver l’équivalent en coordonnées. J’ai utilisé respectivement The Gimp et OpenStreetMap. Ainsi le milieu de la Place Royale se situe aux pixels 1947;1731 et aux coordonnées 2.36554;48.85560 (attention, beaucoup de gens ont la fâcheuse tendance de les donner en lat;lon, alors que la majorité des logiciels préfèrent lon;lat, ce qui correspond à du X;Y).

Une fois que vous avez quelques points (une demi-douzaine doit être bien suffisante), on va créer un fichier GeoTIFF qui est une image géo-tagguée. J’ai utilisé gdal_translate (paquet GDAL de votre distribution GNU/Linux favorite)

.. code-block:: test1

    gdal_translate  -a_srs EPSG:4326 -gcp 4338 4074 2.323681 48.864527  -gcp 170 2069 2.377336 48.865656  -gcp 4940 4975 2.310114 48.868959 -gcp 1626 1112 2.373795 48.851863 -gcp 3566 463 2.3641 48.83893 -gcp 2925 3466 2.34119 48.865739  Plan_de_Turgot.jpg Turgot2.tiff

* -a_srs EPSG:4326 correspond au système de projection que nous utilisons (lon/lat)
* les -gcp indiquent la correspondance coordonnées pixel vers coordonnées terrestres
* Plan_de_Turgot.jpg Turgot2.tiff : fichier d’entrée et de sortie

Génération de tuiles
********************

Toutes (enfin, toutes celles que je connais) les bibliothèques de cartographie JavaScript (Google Maps, OpenLayers, Leaflet, Polymaps…) utilisent des « tuiles » qui sont des images de 256×256 pixels et il faut les générer pour chaque niveau de zoom. Pour cela j’ai utilisé un petit script Python gdal2tiles.py.

.. code-block:: test

    python gdal2tiles.py -p mercator -z ‘12-18’  Turgot2.tiff

* -p mercator : système de projection utilisé. Mercator est généralement utilisé pour les cartes mondiales (Google Maps, OpenStreetMap…)
* -z ‘12-18’ : niveau de zoom à générer. Attention, le niveau 18, ça commencer prendre un peu de temps (une bonne dizaine de minutes)

Mettre tout ça sur une carte
****************************
gdal2tiles.py génère des fichiers tout fait. Donc c’est une version de feignasse, mais qui marche plutot bien. 
J'ai un peu traficoté le code html généré pour OpenLayers mais rien de sorcier.

