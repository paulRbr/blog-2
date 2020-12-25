+++
category = "tech"
date = 2014-04-20
title = "Fibre free sans freebox"
+++

# Version courte

La fibre avec Freebox v5 est limitée à 30 Mbps (mais au moins c’est
symétrique).

Cette limitation disparait avec la Freebox Révolution qui coûte 70€/an.

En se branchant en ethernet, on peut dépasser les 500 Mbps.

On peut aussi utiliser un routeur wifi du commerce à moins de 50€ pour
avoir 200 Mbps. C’est ce que j’explique ici.

# Contexte

Ma première connexion internet, c’était du 28.8 kbps en 1997 à
Madagascar. Notre FAI avait à l’époque une connexion internationale de
2 Mbps.

Je suis chez Free depuis 2005, avec une connexion 2 Mbps initialement.

En arrivant à Paris, j’avais une pauvre connexion 16 Mbps et seulement
0.8 en upload. Mais mon immeuble était fibré par Neuf et les personnes
qui avaient SFR ou Orange avaient la fibre.

Tous les gros coups de pieds dans la fourmilière et le dirigeant qui est
devenu milliardaire en trollant, m’ont fait refuser d’aller voir les
autres concurrents, même pendant les quelques mois où youtube était
devenu inutilisable.

Quand aux FAI associatifs, je soutiens l’idée, mais ma radinerie et mon
manque d’engagement militant ne m’ont jamais fait passer le cap. Après
tout [ma banque](http://www.lanef.com/) et [ma compagnie
d’électricité](http://www.enercoop.fr) sont des coopératives. Pourquoi
pas mon internet ?

En décembre, j’ai reçu un coup de fil de Free pour poser la fibre. Après
un no-show du technicien SFR (apparemment la fibre n’est pas posée par
le FAI dans l’appartement, mais par l’entreprise qui a initialement
fibré l’immeuble), un rendez-vous décalé par moi, la pose de la fibre,
l’intervention du technicien Free pour finir le travail fait à moitié
par le prestataire de SFR, j’ai la Fibre!

# Concours de chibre

La Freebox v5 n’a pas de prise fibre. Free nous fournit donc un petit
boitier qui prend la fibre d’un côté et expose une prise ethernet de
l’autre côté. On peut brancher la freebox dessus et tout fonctionnera
comme avant. Mais on sera limité à 30 Mbps symétrique. Je suppose
qu’aussi bien le matériel que le logiciel ont été dimensionné pour les
20 Mbps de l’ADSL.

On peut aussi se demander pourquoi ne pas brancher le PC sur le port
ethernet du convertisseur. On peut. Mais il y a une subtilité à
expliquer : en sortie de fibre, il y a deux réseaux, un pour internet,
un pour la télévision à rediriger sur le boitier HD. Les flux sont
taggués respectivement avec les vlans 836 et 835. Pour accéder
uniquement au flux internet, installez le paquet vlan de votre
distribution préférée, puis

```
vconfig add eth0 836
dhclient eth0.836 # ou ce que vous utilisez pour le dhcp
```

Ça y est ! Vous avez la plus grosse connexion. Selon les sites de tests,
le débit était entre 500 et 800 Mbps et mon disque dur est trop lent
pour tester si effectivement sur un gros téléchargement je plafonne à
50 Mo/s.

C’est bien, mais j’aimerais autant avoir le wifi. J’ai donc acheté un
petit [routeur wifi](http://wiki.openwrt.org/toh/tp-link/tl-wr1043nd).

# OpenWRT

OpenWRT est un firmware qui permet de libérer vos petits routeurs wifi
et donc avoir bien plus la main dessus. Ça permet aussi des trucs
rigolos comme les [Piratebox](http://pirateboxfr.com/bienvenue/). Je ne
vais pas vous expliquer le flashage et comment faire une installation de
base. Internet est assez riche.

Par contre, j’ai vraiment galéré à configurer, pourtant c’est très
simple. Dans `/etc/config/network`, sur le vlan correspondant au port
WAN (probablement vlan 2), précisez que vous voulez recevoir que les
paquets avec le tag 836. Deux lignes à modifier, une à ajouter.

Avant :

```
config interface ’wan’
    option ifname ’eth0’
    option proto ’dhcp’
[…]
config switch_vlan
    option device ’switch0’
    option vlan ’2’
    option ports ’5 6’
```

Après :

```
config interface ’wan’
    option ifname ’eth0.836’
    option proto ’dhcp’
[…]
config switch_vlan
    option device ’switch0’
    option vlan ’2’
    option vid ’836’
    option ports ’5t 6t’
```

Note : de ce que j’ai vu sur la documentation d’autres modèles, les
ports seront probablement 0 et 1 et non pas 5 et 6 comme chez moi.

Ça y est ! J’ai un peu plus de 200 Megas en symétrique, soit 10 000 fois
plus que ma première connexion internet. Ce chiffres correspondent à une
[limite du routeur](http://wiki.openwrt.org/doc/hardware/performance).

Ça sera bien assez, hein ;)

# Consommation

Un bon point annexe, c’est la consommation d’électricité. Comme toutes
les boxes, la freebox consomme trop. Mesuré avec un wattmètre bon
marché, la freebox consomme 13W auxquels il faut ajouter les 3W du
convertisseur, soit 16W.

Avec le routeur et le convertisseur je suis à 10 W. Alors, évidemment,
le gain de 6W doublé de l’imprécision du wattmètre ça reste pas très
fiable.

Vu que j’ai internet allumé environ 10 heures par jour en moyenne
(beaucoup moins en semaine, beaucoup plus le week-end), ça fait 20 kWh
d’économisés par an, soit
[3 €](http://www.enercoop.fr/Tarifs_484.html) ! Whoo ! Mais pour une
consommation annuelle de 800 kWh, c’est pas si négligeable.

# Bilan

Pfiou, ça fait longtemps que j’avais pas geeké à si bas niveau pour
rien, les 30 Mbps auraient été bien suffisants ;)
