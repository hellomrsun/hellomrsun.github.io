---
layout: post
read_time: true
show_date: true
title:  Design patterns II - Adapter pattern
date:   2013-05-30 06:00:00 +0100
description: Design patterns II - Adapter pattern
img: posts/uncategorized/design-patterns.PNG
tags: [DesignPatterns]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/design-patterns-II-adapter-pattern.html'
---


There are 4 categories of design patterns called Gang of Four(GoF):

- Creational patterns

- Structural patterns

- Behavior patterns

- Concurrency patterns

<!--more-->

Adapter pattern is a structural pattern.

Adapter pattern definition: Convert the interface of a class into another interface clients expect. An adapter lets classes work together that could not otherwise because of incompatible interfaces. The enterprise integration pattern equivalent is the translator.


UML:

![](./../../../assets/img/posts/2013-05-30-adapter-pattern/01.png)


For example, there are 2 targets that 2 different clients expects.

![](./../../../assets/img/posts/2013-05-30-adapter-pattern/02.png)

![](./../../../assets/img/posts/2013-05-30-adapter-pattern/03.png)

![](./../../../assets/img/posts/2013-05-30-adapter-pattern/04.png)
