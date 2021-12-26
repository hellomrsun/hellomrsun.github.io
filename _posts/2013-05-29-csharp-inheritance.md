---
layout: post
read_time: true
show_date: true
title:  C# Inheritance - Class inheritance, Interface implementation
date:   2013-05-29 07:00:00 +0100
description: C# Inheritance - Class inheritance, Interface implementation CSharp
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/csharp-inheritance.html'
---

Inheritance, Polymorphism and Encapsulationare the three most important concepts in OOP.


Inheritance enables you to create new classes that reuse, extend, and modify the behavior that is defined in other classes. The class whose members are inherited is called the base class, and the class that inherits those members is called the derived class. 


A derived class can have only one direct base class. However, inheritance is transitive. 

A class can implement multiple instances.


I will show two examples of inheritance which are :

- Class inheritance
- Interface implementation



1) Class inheritance

A parent class with 2 constructors and 1 method:

![](./../../../assets/img/posts/2013-05-29-inheritance/01.png)

A child class heritate the parent class and communicate with parent class.

![](./../../../assets/img/posts/2013-05-29-inheritance/02.png)

Test them, the results are shown on the right of code.

![](./../../../assets/img/posts/2013-05-29-inheritance/03.png)


2) Interface implementation


Here I've declared two interfaces with some methods signatures. 
PS: An interface contains only the signatures of methods, delegates or events, and of course properties.

![](./../../../assets/img/posts/2013-05-29-inheritance/04.png)

Then a class implement these two interfaces with respective different implementation of every methods and properties declared. You should notice that, to distinguish the different implementations, the interface name should be ahead of the every single implementation of method if they have same names.

If they don't have same names, you just need to use "Public" ahead of the property or method, and you don't need to use interface as prefix.

![](./../../../assets/img/posts/2013-05-29-inheritance/05.png)


Then the first 3 lines are to test the common implementations of methods.

Then the second and third parts are to test the method implementations for each interface.

![](./../../../assets/img/posts/2013-05-29-inheritance/06.png)

I hope you can find this article helpful. Enjoy coding!