---
layout: post
read_time: true
show_date: true
title:  Multi-layer project architecture
date:   2015-02-08 08:00:00 +0100
description: Multi-layer project architecture, N-Tier
img: posts/uncategorized/architecture.png
tags: [Architecture]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/multi-layer-project-architecture.html'
mathjax: yes
redirect_from:
  - /2015/02/08/multi-layer-project-architecture.html
---


I’ve been worked recently on the project structure refactoring. A good project structure could give you a good visibility and a clear understanding even you are brandly new in a project, and make your further development much easy.

Some practices could be applied to increase the project maintainability and facilitate the development in the team if there are multiple projects and multiple solutions.

<!--more-->

I would like to introduce some advice based on my own experience.

- Manage common package (using Nuget)

It’s very practical when you have multiple solutions in your team. You can manage to use the same version of tools or packages in the whole application to ensure the consistence.

- Separate projects with sub-folders physically and create identical virtual folders.

For example, you can organize your solution with the following sub folders.

<br/>

- ExternalReferences: all your references from other solutions.
- Libraries: your projects shared to all layers
- PresentationLayer: this could be ASP.NET projects, WPF projects,Window Forms projects.
- ServiceLayer: it contains different services to provide different functionalites to presentation layer.
- BusinessLayer: it includes business logics.
- DataAccessLayer: a centric layer to manager all the data access in your projects
- UnitTests: include your unit tests
- IntegrationTests: as integration tests could be complicated and take long time. It’s preferred to have a dedicated project for it.

<br/>

The project organization really depends on the product you are developing. A good project organization can make your development much easier. So before development a project, take a little time to well conceive its organization.

I hope you find this article helpful! Thanks.