---
layout: post
read_time: true
show_date: true
title:  Software Craftsmanship - Software Development Pinciples
date:   2013-07-05 08:00:00 +0100
description: Software Craftsmanship - Software Development Pinciples, developer
img: posts/uncategorized/craftsman.PNG
tags: [Craftsmanship]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/software-craftsmanship-software-development-principles.html'
---


### SOLID principles:

- Single Responsibility Principle (SRP): 

A class or an interface should have only one responsibility.

A class with "And" doesn't respect this rule.

<!--more-->

- Open/Closed principle (OCP):

A class is open for extension, but closed for modification.

This means when a new functionality is coming, you should not modify the existing code or minimize modifications, but extend the existing code.


- Liskov Substitution principle (LSP):

It means when a base class is used, its derived class can replace it.


- Interface Segregation principle (ISP):

ISP means split general interfaces into more small specific interfaces.


- Dependency Inversion principle (DIP):

High level modules should not depend upon low-level modules. Both should depend upon abstractions.
Abstractions should never depend upon details. Details should depend upon abstractions.

IoC Inversion of Control includes Dependency Injection.

Dependency Injection includes Constructor Injection, Setter Injection.



### DRY: Don't Repeat Yourself

The principle is : Don't allow code duplication.


### YAGNI: You Aren't Gonna Need It.

The principle is : Don't add new functionality until deemed necessary. This is a XP practice.


### KISS: Keep It Simple, Stupid!

You will be able to solve more problems, faster.

You will be able to produce code to solve complex problems in fewer lines of code

You will be able to produce higher quality code

You will be able to build larger systems, easier to maintain

You're code base will be more flexible, easier to extend, modify or refactor when new requirements arrive

You will be able to achieve more than you ever imagined

You will be able to work in large development groups and large projects since all the code is stupid simple


### XP Extreme Programming practices:

- Pair programming: one person for implementation detail, the other for code review and global picture
- Refactoring
- Testing (TDD)
- Continuous Integration
- Coding Standard
- Simple Desgin
- User stories
- Small releases
- Collective ownership
