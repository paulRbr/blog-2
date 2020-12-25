+++
category = "tech"
date = 2013-09-21
title = "Short history of routes computation"
slug = "short-history-of-routes-computation"
+++

# Introduction

I wrote a blog post in French that had some unexpected success (by
success I mean that people actually read it). At least two people asked
for an English translation. So here it goes, with some of the errors in
the French version corrected.

Formally we would speak of "shortest path in a graph problem". The goal
is the same: what is the shortest way to go from A to B.

Route computation are nice as the actual use cases can be explained to
anyone =

-   the GPS end user
-   the computer science student that at some point learnt the basic
    algorithms
-   there is still research going on, but it can be explained to anyone
    interested within a few pints

Personally, what I find interesting is how those algorithms evolved
through time. Sorry for punctual technical details.

# 1956 — 1958: Ford, Moore and Bellman

The first suggested algorithm was published independently by those
authors.

It is nowadays usually called the *Bellman-Ford* algorithm.

# 1959: Dijkstra

[Edgard Dijkstra](https://en.wikipedia.org/wiki/Edsger_W._Dijkstra) is
Dutch.

He is one of the big names in computer science. He is know for his
handwriting and quotes such as:

-   `Simplicity is prerequisite for reliability`
-   `The question of whether Machines Can Think… is about as relevant as the question of whether Submarines Can Swim`
-   `Object-oriented programming is an exceptionally bad idea which could only have originated in California`

He is the author of — brace yourself — *Dijkstra’s algorithm*
published in 1959. It has been described in a [two pages only article](http://www-m3.ma.tum.de/foswiki/pub/MN0506/WebHome/dijkstra.pdf)
but the name stuck as the fundamental brick of route computations.

However, the algorithm we learn at school is not the one published by
Dijkstra. It has a complexity of O(n²) while we are taught that
complexity of the algorithm is O(n·log(n)).

We had to wait 28 years to get to it.

# 1987: Tarjan

The weakness of Dijkstra’s algorithm is its priority queue that returns
what node to visit next. An [article from 1987](http://www.cs.princeton.edu/courses/archive/fall03/cs528/handouts/fibonacci%20heaps.pdf)
by Tarjan (an other reference in the world of graphs) brings us to the
"modern" Dijkstra’s algorithm.

Many variations have been tested to speed up the algorithm with
mitigated success, such as A\*, bi-directional searches, sacrificing the
optimality or a combination of all that.

On a recent computer, computing a route across France takes around a
second. Therefor back in the 90’s it was way to slow. There was a need
to speed up the computation.

We had to wait 18 year to get to it.

# 2005: Dimacs challenge and rise of the KIT

The [9th Dimac Challenge](http://www.dis.uniroma1.it/challenge9/format.shtml) was about
routes computation. For this event the [road network of the United States](http://www.dis.uniroma1.it/challenge9/download.shtml) was
published.

A large number of publications pulverised all the records. The
algorithms are now fast enough to compute a route between two points on
earth in less than a millisecond (more than a *thousands* times faster
than the Dijkstra’s algorithm).

An overwhelming share of publications come from from the [Karlsruhe Institute of Technology](http://i11www.iti.uni-karlsruhe.de/en/projects/route_planning/index).

The team members suggested many algorithms, but also tested nearly every
possible combination between those algorithms.

There were so many publications it was hard to know where to look.

# 2008: consolidation with the Contraction Hierarchies

After this phase of exuberant creativity, we could extract the core
substance to make the algorithm that will probably become the new
reference = the *contraction hierarchies*.

It has been presented in a master thesis (so I am somewhat ashamed of my
PhD thesis…) by
[Geisberger](http://algo2.iti.kit.edu/documents/routeplanning/geisberger_dipl.pdf).

There is nothing really new, only the removal of superfluous ideas that
made other algorithms too complicated to keep the smallest core that
works well.

Everybody that is interested in algorithmic should read the algorithm
and its demonstration of optimality. The first time I read it, I could
not grasp how it worked. I had to walk through the demonstration to be
convinced.

That algorithm is used in [OSRM](http://map.project-osrm.org/), a free
route calculator based on [OpenStreetMap](http://www.openstreetmap.org)
data.

# 2009: public transit are still forgotten

At last we know to efficiently compute a route on a street network. What
about public transit? Not so bright here.

The question was already studied in 1991 in the great PhD thesis of
Eduard Tulp. But little happened since.

Performances are deceiving and trying to use the successes in street
network failed.

In the article [Car or Public Transport—Two
Worlds](http://link.springer.com/chapter/10.1007/978-3-642-03456-5_24)
H. Bast show the differences that exist between both means of
transportation and that is not interesting to try to use the same
techniques.

# 2010: transfer patterns, performance, at last!

It was summer, I had just sent my thesis manuscript to the examiners.
Because of over-zealousness I read the [latest article from H. Bast](http://ad.informatik.uni-freiburg.de/files/transferpatterns.pdf).

For the first time it was possible to compute routes using public
transit within a few milliseconds in a large city as New-York.

If you looked closely, the was still a slight twist: the authors used
the computing power of thousands of computers from Google. A massive
pre-processing is the key to such good results.

Just two more years to wait to have an effective algorithm.

# 2012: Delling’s Raptor

Daniel Delling likes cool names (a previous algorithm was called
*Sharc*). He chose
[Raptor](http://research.microsoft.com/apps/pubs/default.aspx?id=156567)
for his new algorithm.

The proposed approach has no need for pre-processing and has better
performances than the transfer patterns.

Hooray! Cars do not have the monopoly on efficient algorithm any more.
Raptor has the advantage to be rather simple and to have nice properties
(too technical to bother you with them).

![Zoidberg from Futurama saying hooray](../images/zoidberg_hooray.webp)

# Intermission: opendata and science

Science needs data to be easily available. The DIMACS challenge was a
success because big real life data set were published.

It took six years from the first high-performance street network routing
algorithm to the first high performance algorithm on public transit. We
had to wait so long until data sets were at last released.

It is the opendata movement applied to transportation that allowed that
scientific progress.

# 2013: Connection Scan Algorithm

A last one! In an article very modestly called [Intriguingly Simple and Fast Transit Routing](http://link.springer.com/chapter/10.1007%2F978-3-642-38527-8_6)
the authors present the *connection scan algorithm*. It is slightly more
efficient than Raptor but is considerably more simple.

When reading the article, and once again when implementing it, I was
struck how brain dead simple it is, but it works.

We went through 57 years of research to end up with an algorithm that
could have been written at the same time as Dijkstra’s.

Hence a last quote of Dijkstra that seems very appropriate:

> Simplicity is a great virtue but it requires hard work to achieve it and education to appreciate it. And to make matters worse: complexity sells better
