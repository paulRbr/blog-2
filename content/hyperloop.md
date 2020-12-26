+++
category = "vert"
date = 2013-08-12
title = "Hyperloop, un mode pas si révolutionnaire que ça"
+++

{% update(date="2020-12-26") %}
Plus de 6 ans plus tard, le projet ne semble toujours pas avoir abouti.

Pendant ce temps, les TGV vont avoir 20% de capacité en plus (locomotives plus courtes permettant d’avoir une voiture en plus, plus de seconde et mois de première).

La ligne Paris-Lyon, la plus saturée, va passer à 16 trains par heure et par sens (en particulier grâce à une nouvelle signalétique)
{% end %}

Après plusieurs semaines de teasing, on en sait un peu plus sur le
projet *hyperloop*.

[Elon Musk](http://fr.wikipedia.org/wiki/Elon_Musk) est un milliardaire
qui a fait fortune avec Paypal, qui croit dur comme fer que le futur
c’est demain, et que ce futur sera rempli de fusées
([SpaceX](http://fr.wikipedia.org/wiki/SpaceX)), de voitures écolo
([Tesla](http://fr.wikipedia.org/wiki/Tesla_Motors)) et d’avions
hypersonics.

Il s’est dit très déçu par le projet de [ligne à grande vitesse en
Californie](http://en.wikipedia.org/wiki/California_High-Speed_Rail) :
trop lent, trop cher. Pas à la hauteur de la gloire de l’Amérique !

Il s’est donc décidé à concevoir un système qui irait vite (proche de la
vitesse du son) pour un prix d’infrastructure dix fois moins cher.

Tout dédaigneux que je sois, j’étais quand même curieux et parce que
j’ai la capacité de me passionner pour les aspect techniques sur des
produits que je méprise (moteurs à explosion, réacteur nucléaire…). Et
puis vues les réalisations du personnage, je ne pouvais pas snober
l’évènement.

J’ai donc pris ce document, et je l’ai parcouru
<http://www.spacex.com/sites/spacex/files/hyperloop_alpha-20130812.pdf>.

Voici ce que j’en ai retenu. C’est une réaction à chaud, et j’espère ne
pas dire trop de bêtises que je regretterai.

# Résumé technique

1.  On créé un grand grand tuyau, dont la pression de l’air est faible
    (pas sous vide, ça coute trop cher)
2.  On fait circuler à l’intérieur des _pods_ de 28 passagers avec un gros
    ventilateur pour chasser le peu d’air qui reste
3.  Très espacés, des moteurs linéaires ré-accélèrent la capsule

En pointe ça circule à 1200km/h.

# Capacité très faible

D’après l’auteur, la capacité de l’installation est d’une capsule toutes
les 2 minutes, soit 840 passagers par heure.

Comparons ça à une ligne TGV existante. Les [TGV
Duplexe](http://fr.wikipedia.org/wiki/TGV_2N2) on une capacité de 509
personne (plus une 50-aine de squatteurs de strapontins et voiture bar).
Ces TGV roulent en heure de pointe en unités doubles, soit plus de 1000
passagers.

En heure de pointe, il y a plus de 10 trains par heure dans chaque sens.

Une ligne traditionnelle de grande vitesse nécessite peut-être dix fois
moins d’investissement, mais est capable de transporter quinze fois plus
de passagers.

Le projet de ligne à grande vitesse prévoit jusqu’à 260 000 passagers
par jour. En espérant que les passagers veuillent bien s’étaler
uniformément dans la journée, il faudra quand même une capacité de 5000
passagers par heure et par sens.

# Consommation d’énergie significative

Malgré la faible pression, la consommation d’énergie est significative.
L’ensemble du système doit consommer 21 MW en continu (sur la ligne Los
Angeles-San Francisco) pour 34 capsules en mouvement, soit 952
passagers, soit 22 kW de consommation *moyenne* par passager.

La puissance en *accélération* maximale des TGV cités précédemment, est
de 9,2 MW pour 509 passagers. Soit 18 kW de consommation *maximale* par
passager.

Évidemment, un TGV est beaucoup plus lent. Mais je voulais juste
signaler que la consommation d’énergie n’est pas aussi faible que ce que
le projet vend.

En ce qui concerne l’alimentation entièrement par des panneaux
photovoltaïques, en recouvrant toute la [LGV
Paris-Lyon](http://fr.wikipedia.org/wiki/LGV_Sud-Est), on obtient `409 km
× 13m × 120W/m² = 638 MW`. De quoi produire environ 0,7 TWh par an, soit
10% de la consommation de la SNCF. Sachant qu’il y a 2000 km de lignes à
grande vitesse en France et 29 000 km au total, on pourrait également
couvrir toute la consommation de la SNCF en couvrant les lignes de
panneaux photovoltaïques.

Ne m’embêtez pas avec les détails de stockage, Hyperloop ne le fait pas
non plus.

# Les petits secrets

Tout comme la voiture à air comprimé consomme très peu que parce qu’elle
est très légère avec un moteur à faible puissance, les performances de
hyperloop ne sont atteinte qu’à grands coups de downscaling.

Il n’y a pas de toilettes, pas de wagon restaurant… c’est déjà de la
place économisée.

Il n’y a pas non plus de première classe : les capsules font 1,35 mètre
de large pour deux sièges de front. Un TGV fait 2,90 m de large pour 4
places de front (mais par honnêteté, je vais rappeler l’existence d’un
couloir dans les TGV).

En classe unique, sans wagon bar, sans toilettes, on pourrait dépasser
les 600 passagers que transporte une rame de Ouigo.

Tout cela permet de descendre à environ 460kg de capsule par passager,
contrairement 770 kg sur un TGV.

Ce poids est un des grands axes pour réduire la consommation (ou
augmenter la vitesse) des trains à grande vitesse dans le monde entier.

# Conclusion

C’est un projet rigolo, qui va très vite à condition que ça soit réservé
à une minorité puisque le projet ne peut pas passer l’échelle.

Je pense qu’il y a de la part de l’auteur des préjugés envers le
systèmes ferroviaire traditionnel — on parle d’un constructeur de
voitures de sport — et qu’il en sous-estime les avantages.

Pour votre bilan énergétique, ça reste bien évidemment mieux qu’une
voiture électrique, mais moins bien qu’un car au diesel ou un bon vieux
TGV qui roule tranquillement à 300 km/h pour avoir le temps d’admirer le
paysage.

J’espère en tout cas que si c’est mis en place sur des Paris → Helsinki,
que ça soit bientôt. Avant que j’aie des problèmes à me retenir et que
je sois obligé d’avoir une bouteille vide si l’envie me prend d’aller
aux toilettes au cours des 3 heures de trajet.
