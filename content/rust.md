+++
date = 2013-04-17
title = "Rust un langage prometteur"
category = "tech"
+++

{% update(date="2020-12-26") %}
Ze suis toujours aussi fan du Rust et j’ai pu en faire professionnellement. Et ce blog a été réécrit en utilisant
[zola](https://www.getzola.org/).

Par contre, l’évolution est amusante : presque tout ce que je détaille n’est plus d’actualité, d’autres approches ont été utilisées.

Mais reste le plus important : on a une alternative au C++ sûre et plaisante à utiler.
{% end %}

Je me suis intéressé au langage [Rust](http://www.rust-lang.org/). Et je
pense qu’il mérite que vous vous intéressiez également. Le problème
c’est que je me suis un peu emballé et cet article est devenu un peu
trop ambitieux. J’espère qu’il reste compréhensible malgré les
approximations généreuses.

J’ai donc décidé de ne pas parler de la syntaxe, mais des deux aspects
que je trouve particulièrement intéressants :

-   La gestion du parallélisme
-   La gestion de la mémoire

# Gestion du parallélisme

Utiliser le mot *parallélisme* est risqué : je risque de me faire taper
par ceux qui s’y connaissent. Mais j’aime vivre dangereusement, c’est
mon côté rebelle.

La question de fond, c’est comment faire plusieurs choses en même temps : gérer plusieurs requêtes http, commencer à parser le texte pendant
qu’on lit sur le disque dur la suite, avoir plus de fps à Wolfenstein,
etc.

Des approches, il y en a plein ! Le problème permanent c’est comment
faire communiquer ces bouts de code qui tournent côte à côte.

## Multiprocess

On lance plusieurs fois le programme. Approche très simple et souvent
utilisée sur des serveurs qui se dédoublent pour gérer plus de requêtes.
La communication entre les process est galère… De plus lancer un
nouveau process est une opération lourde à ne pas faire trop souvent.

## Multithread

C’est ce que nous apprenons à l’école. On apprend à utiliser des mutex,
des sémaphores, on deviens fou à essayer de déboguer une
*race-condition*. Donc c’est non seulement difficile à coder, mais en
plus un bon nombre de langages on du mal à implémenter les threads. Et
en plus, dans le cas de gros serveurs, créer un thread par requête est
déjà une opération trop lourde, on arrive au [C10K
problem](http://www.kegel.com/c10k.html).

## Boucle d’évènements

[node.js](http://nodejs.org) est capable de gérer un grand nombre de
requêtes en parallèle tout en ne tournant qu’un seul thread. Cela a
popularisé les boucles d’évènements. Une boucle qui gère l’ensemble des
tâches à traiter fonctionne plutôt bien ; en particulier lorsqu’il y a
un grand nombre de temps morts comme des lectures disques, requêtes à
une base de données, etc..

Cet article explique plutôt bien ce dont il s’agit
<http://applidium.com/en/news/writing_an_evented_web_server/>.

## Les tasks Rust

Les *tasks* dans Rust sont comparables que les *goroutines* de Go. La
création d’une tâche est très légère : c’est tout à fait envisageable de
lancer des dizaines de milliers de tâches. Concrètement, à l’exécution
du programme plusieurs threads sont lancés qui se répartissent le
traitement des tasks.

En ce qui concerne la communication entre taches, un objet spécifique
permet de s’échanger des données. Il s’agit de l’unique moyen de
communiquer entre tâches : il n’y a donc aucun moyen d’avoir deux taches
qui accèdent simultanément à la même donnée. Il n’y a donc plus toutes
les emmerdes liées à la programmation multithreadée.

# Gestion de la mémoire

Aaaaahhh que de trolls Java vs. C++ vs Alzheimer.

L’approche de Rust sur la gestion de la mémoire est particulièrement
intéressante car ça doit être la seule qui arrive à gérer tous les cas
d’utilisation du C++ (en particulier dans sa version 2011) en apportant
une grande sécurité et permettant de très bonnes performances.

Par sécurité j’entends quatre choses :

-   Pas de valeur nulle (impossible d’avoir une `NullPointerException`)
-   Pas de fuite mémoire
-   Pas d’accès à la mémoire là où on n’a pas le droit
-   Pas d’accès concurrent

Rust répond à cette problématique en proposant trois manière de
référencer de la donnée (le C++ en ayant 4 depuis les R-values du C++11,
et encore je ne compte pas les smart pointers, etc.).

## Garbage collection

Une approche basée sur des garbage collectors considère globalement que
tout est pointeur et qu’il y a un éboueur global qui sait combien de
variables pointent sur l’objet. Il y a un problème de performance et les
pointeurs peuvent être nuls ce qui empêche d’être sur que l’on peut
accéder à l’objet. Et je parle même pas des horreurs autour du boxing.

Rust propose des données qui seront garbage-collectées. Il suffit de
préfixer le type par un `@`. Il est obligatoire d’initialiser les
données et ces données ne peuvent en aucun cas être partagées entre deux
*tasks*. De ce fait, le garbage collector ne pénalise qu’une seule
*task* et pas toutes. De plus, on a la garantie qu’il est impossible que
deux *tasks* accèdent simultanément à la même donnée. Il n’y a donc
aucun risque d’accès concurrents.

## Données locales

Pour des raisons qui m’échappent, peu de langages proposent de déclarer
des objets qui ont une durée de vie limitée au scope. C’est extrêmement
performant (pas de garbage collector, pas de surcout mémoire lié au
pointeur…). On a la garantie que l’objet existe et il sera simplement
détruit à la fin du contexte. Si on veut sortir une variable du
contexte, on la copie.

Les défenseurs du C++ vanteront cette approche nommée
[RAII](http://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization)
qui est vraiment géniale de simplicité.

Il y a juste un défaut : lors qu’on souhaite avoir plusieurs objets qui
font référence à un même objet, ça se gâte (mais en pratique, en prenant
le temps de bien développer, il s’agit de cas limite assez rare).

Il s’agit là du modèle de base en Rust, autant dire que ça me réjouit.

## Owned boxes

C’est le terme utilisé dans Rust. Il s’agit d’un pointeur similaire à un
`std::unique_ptr` en C++. Il doit être initialisé (pas de pointeur nul)
et il ne peut pas y avoir deux pointeurs qui pointent sur le même objet.
Un bout de code **possède** la mémoire. Du coup la gestion de la mémoire
est triviale et il n’y a pas besoin de garbage collecteur.

La possession peut être transmise (typiquement vers une autre *task*),
mais il n’est plus possible d’utiliser la première variable (les
C++-istes penseront à `std::move`).

```
fn main() {
  let x = ~10; // x est un owned box vers un entier
  let y = x; // y prend la possession. x n’est plus utilisable
  io::println(int::str(*x)); // Ça ne compilera pas : on n’a pas le droit d’utiliser x
}
```

## Mot de la fin sur la mémoire

Ça peut sembler compliqué d’avoir ces trois notions. Surtout lorsqu’on
vient d’un langage tel le Java où l’on ne se pose pas forcément la
question.

Je pense que c’est quand même utile de se pencher sur ces problématiques
de possession des objets et que l’approche Rust est très agréable.

# Autres choses que j’aime bien

Il y a d’autres détails que j’aime bien en Rust, les voici en vrac :

-   Le compilateur se base sur [LLVM](http://fr.wikipedia.org/wiki/LLVM)
    ce qui évite de réinventer la roue pour les optimisations à la
    compilation
-   Par défaut on a que des constantes. Il faut explicitement demander
    des variables mutables
-   Il n’y a pas d’héritage lourdingue à la Java. Tout se base sur des
    interfaces. Cependant il faut encore que je creuse cet aspect. Ça
    m’irrite de devoir définir explicitement les interfaces qu’on
    implémente
-   Le nom, même si c’est galère à chercher sur Google (moins que Go
    cependant)

# Conclusion

Ça fait longtemps que la complexité du C++ m’agace, mais je n’ai pas
trouvé de langage qui me satisfait. Il y a bien le D, mais j’ai le
sentiment qu’il reste trop proche du C++ sans apporter tant de
simplifications que ça. Le Go est un très bon candidat, mais peut-être
pas assez brut…

Rust a réussi à avoir une gestion de mémoire très rigoureuse, avec un
bon compromis performances/nombre de concepts. Seule la sécurité n’a pas
été sacrifiée et c’est fortement appréciable.

Malheureusement, ce n’est pas vraiment utilisable en production car
l’évolution est encore assez rapide. J’ai hâte qu’une version 1 sorte et
que j’aie l’occasion de m’en servir pour un vrai projet.

Si vous voulez l’essayer, il est conseillé d’utiliser la branche
*master* de leur dépôt GitHub. La communauté est très sympathique sur
IRC, donc n’hésitez pas à demander si vous coincez.
