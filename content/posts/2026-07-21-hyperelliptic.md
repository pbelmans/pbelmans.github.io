---
title: "Hyperelliptic varieties: quotients of complex tori by finite groups"
slug: hyperelliptic
date: 2026-07-21
tags:
- algebraic geometry
- programming
categories:
- mathematics
---

There is a new website, **[hyperelliptic.ncag.info](https://hyperelliptic.ncag.info)**,
on the classification of hyperelliptic (or *generalized hyperelliptic*) varieties
in complex dimensions 2, 3 and 4. For now it lives as a subdomain of ncag.info.

A hyperelliptic variety is a quotient $X = T/G$ of a complex torus $T$ by a finite
group $G$ acting freely and without translations. In dimension 1 these are the
elliptic curves, in dimension 2 the seven bielliptic surfaces of Bagnera and De
Franchis; the word has nothing to do with hyperelliptic *curves*. The remarkable
thing is that all the numerical invariants (the Hodge diamond, the order of the
canonical bundle, the number of moduli, the irregularity, the polyvector fields,
the twisted Hodge numbers, the Hochschild cohomology) depend only on the tangent
representation $\rho\colon G \to \mathrm{GL}(V)$, and can be read off from its
character theory. The website computes them all with
[OSCAR](https://www.oscar-system.org/), for every group in the classifications of
Uchida–Yoshihara, Lange and Catanese–Demleitner (dimension 3) and of Demleitner
(the 79 groups in dimension 4).

This all started from a collaboration with
[Andreas Demleitner](https://www.math.uni-bielefeld.de/~ademleitner/) and Pedro
Núñez on [the Albanese morphism for these varieties](https://arxiv.org/abs/2411.14814).
Working on that paper I learned a great many things about hyperelliptic varieties
from Andreas, and this website is in a sense a place to keep all of it: the
invariants we computed by hand, and many more, now generated automatically and
cross-checked against the literature.

As with my other websites it is a static site built (using LLMs) with
[Hugo](https://gohugo.io). Feature requests, corrections and contributions are
very welcome, on [GitHub](https://github.com/pbelmans/hyperelliptic.info) or by
email.
