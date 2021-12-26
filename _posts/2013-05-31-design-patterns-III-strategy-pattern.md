---
layout: post
read_time: true
show_date: true
title:  Design Patterns III - Strategy pattern
date:   2013-05-31 08:00:00 +0100
description: Design Patterns III - Strategy pattern
img: posts/uncategorized/design-patterns.PNG
tags: [DesignPatterns]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/design-patterns-III-strategy-pattern.html'
---

Strategy pattern principle is create a interface strategy with methods definitions. The concrete strategies will implement the interface. And context will use interface strategy. With different strategy contexts, different strategies will be called.


UML:

![](./../../../assets/img/posts/2013-05-31-strategy-pattern/01.png)

<!--more-->

Implementation:

There is an interface who is the strategy, it defines a method signature. 

Two concrete class implement it and its method.

In a context class, it uses interface strategy as its parameter in its constrcutor. Its execute strategy method will call the interface strategy method.

![](./../../../assets/img/posts/2013-05-31-strategy-pattern/02.png)

Usage of strategy:

![](./../../../assets/img/posts/2013-05-31-strategy-pattern/03.png)
