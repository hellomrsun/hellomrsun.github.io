---
layout: post
title: Design patterns - Singleton, Double-Check Locking Singleton and Lazy initialization
excerpt_separator:  <!--more-->
tags: Design-Patterns
canonical_url: 'https://sunjiangong.com/design-patterns-singleton-double-check-locking-singleton-lazy-initialization/'
---

Design patterns are a collection of software development best practices in solving commonly occurring problems.

Design patterns' purpuse is to improve the software's quality, reusability, and maintenability.

<!--more-->

There are 4 categories of design patterns called **Gang of Four** (GoF):

- Creational patterns
- Structural patterns
- Behavior patterns
- Concurrency patterns


**Singleton** is a creational pattern. 

**Double-checked locking** is a concurrency pattern.

**Lazy initialization** is a a creational pattern.


Singleton is a design pattern used to limit one class to have just **only 1 instance**.



**Basic Singleton** example:


![](./../../../assets/images/Singleton/basic_singleton.png)


<br/>

**Double-check locking singleton** example:

volatile: ensures that one thread retrieves the most up-to-date value written by another thread.

![](./../../../assets/images/Singleton/double_check_locking_singleton.png)


<br/>

**Lazy initialization singleton** example:


![](./../../../assets/images/Singleton/lazy_initialization_singleton.png)


<br/>

Call the methods inside the singleton classes.

![](./../../../assets/images/Singleton/call.png)

<br/>

The two implementations of singleton works, and you can choose the ideal one with your special requirements. 


I hope this post does help to you. Enjoy coding!

<br/>

**References:**

http://csharpindepth.com/Articles/General/Singleton.aspx

http://en.wikipedia.org/wiki/Design_pattern_%28computer_science%29#Classification_and_list

