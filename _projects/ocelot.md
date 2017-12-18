---
layout: page
title: ocelot
description: a tests case generation tool for C
img: /assets/img/ocelot.jpg
---

OCELOT (**O**ptimal **C**overage s**E**arch-based too**L** for s**O**ftware Testing) is a new test suite generator tool for C programs implemented in Java. Unlike previous tools for C programs, OCELOT automatically detects the input types of a given C function without any specification of parameters. In addition, the tool handles the different data types of C, including structs and pointers and it is able to produce test suites based on the [Check][check] unit testing framework.

OCELOT implements several meta-heuristics algorithms, included LIPS (Linearly Independent Path-based Search), designed to efficiently use the search budget and re-use profitable information from previous iterations.

OCELOT had been developed with the support of a research grant by me and [Simone Scalabrino][simone] with the supervision of [Dario Di Nucci][dario] starting from March 2015.

Stay tuned! The tool will be soon released on GitHub!

P.s: we have an amazing logo 😎!

[check]: https://libcheck.github.io/check/
[dario]: https://dardin88.github.io
[simone]: https://dibt.unimol.it/staff/sscalabrino/home

![](/assets/img/ocelot.png)


