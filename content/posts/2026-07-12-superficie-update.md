---
title: "le superficie algebriche: a table and more surfaces"
slug: superficie-update
date: 2026-07-12
tags:
- algebraic geometry
- programming
categories:
- mathematics
---

Back in 2015, [Johan Commelin](https://math.commelin.net) and I made
**[le superficie algebriche](https://superficie.info)**, an interactive picture of
the geography of minimal complex algebraic surfaces, plotted by their Chern
numbers $\mathrm{c}_1^2$ and $\mathrm{c}_2$ (see the
[original post](/blog/2015/07/15/le-superficie-algebriche/) and a
[2019 update](/blog/2019/12/12/update-to-superficie-algebriche/)). It has just had
its biggest update since.

**A table.** Next to the plane of Chern numbers there is now a
[table](https://superficie.info/table/): every class of surface in the database
with its Kodaira dimension and numerical invariants, sortable by any column,
searchable by name, and with descriptions you can unfold in place.

**More surfaces, with descriptions and references.** A literature sweep added a
long list of named classes, from fake quadrics and the ball quotients on the
Bogomolov–Miyaoka–Yau line (Ishida, Cartwright–Steger, Yeung's surface of maximal
canonical degree) to product-quotient and Beauville-type surfaces. Each now comes
with a short description, what it is and why it is interesting, and full citations
resolved to MathSciNet, arXiv or DOI, using the same bibliography machinery I built
for [mgnbar](/blog/2026/07/09/mgnbar-update/).

**The map, filled in.** The whole interior between the Noether line and the
signature-zero line is now populated (following Persson), so the picture genuinely
shows which Chern numbers occur and, just as clearly, the thin strip below the
Bogomolov–Miyaoka–Yau line that is still an open problem.

Smaller things: the holomorphic Euler characteristic of the tangent bundle
$\chi(\mathrm{T}_S)$ is shown too, and every surface now has its own URL, so you
can link straight to one, like
[superficie.info/2/4-8/fake-quadrics](https://superficie.info/2/4-8/fake-quadrics).
As with my other websites it is now a static site built with
[Hugo](https://gohugo.io).

Corrections and, especially, more surfaces are very welcome, on
[GitHub](https://github.com/superficie/superficie-algebriche/issues) or by email.
If you know a surface that belongs on the map, it is easy to add.

<hr>

LLMs were used to build this, which made the whole process *much* faster.
