---
title: "A better environment manager for Python?"
date: 2023-11-03T12:00:00+01:00
draft: false
weight: 60
---

Over the last year I've started using the Poetry tool for managing Python virtual environments and project dependencies. It's a wonderful piece of software and makes dependency management atomic to each project, and relatively pain-free. Unfortunately the way Python package metadata is designed can make it difficult to resolve dependency conflicts. Sometimes the only way to effectively resolve dependency conflicts is for Poetry to repeatedly download different versions of a package and test for conflicts against other packages. If there is a conflict, it can create a combinatorial nightmare. Even on decent internet connections the process can take several hours and becomes a major blocker. Poetry does its best to fix this, but it's a fundamentally hard/impossible problem to solve. Worse still, often the dependencies in conflict do not cause breaking problems, and other package managers like pip would ignore them and carry on installation none the wiser.

As a temporary hack and fun mini-project I've built an [alternative environment manager called Noetry](https://github.com/JHart96/noetry) (get it?) that essentially wraps pip in a nice user interface similar to Poetry. It doesn't do anything clever like Poetry does, but it does have a few features I'd love to see in Poetry in the future:

* Fast dependency resolution - same as pip: quick, no hassle, no repeated large file downloads
* Python version selection - using Pyenv under the hood to manage Python versions on a per-project basis
* `requirements.txt` conversion - sometimes you don't need all of the features of Poetry (e.g. for CI/CD app deployment) and converting to a requirements file can be really useful. **Note** Poetry does have this but it doesn't produce a standard requirements file and I've had trouble using it in practice.

This project is designed to be a bit of fun (hence the daft name), and I won't be maintaining it or recommending anyone to use it seriously. That said I would love to see a tool that fills the same niche, but with a rigorous dependency resolver, simple installation, and minimal hassle. 