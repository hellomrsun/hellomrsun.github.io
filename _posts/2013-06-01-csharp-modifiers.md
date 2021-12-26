---
layout: post
read_time: true
show_date: true
title:  C# modifiers
date:   2013-06-01 08:00:00 +0100
description: C# modifiers
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/csharp-modifiers.html'
---

### Access Modifiers:

- public
- private
- internal
- protected

<!--more-->

### Modifiers:

- abstract: Indicates that a class is intended only to be a base class of other classes.
async: Indicates that the modified method, lambda expression, or anonymous method is asynchronous.

- const: Specifies that the value of the field or the local variable cannot be modified.

- extern: Indicates that the method is implemented externally.

- event: Declares an event.

- in: For generic type parameters, the in keyword specifies that the type parameter is contravariant. You can use the in keyword in generic interfaces and delegates.

- out: For generic type parameters, the out keyword specifies that the type parameter is covariant. You can use the out keyword in generic interfaces and delegates.

- new: Hides an inherited member from a base class member.

- override: Provides a new implementation of a virtual member inherited from a base class.

- partial: Defines partial classes, structs and methods throughout the same assembly.

- readonly: Declares a field that can only be assigned values as part of the declaration or in a constructor in the same class.

- sealed: Specifies that a class cannot be inherited.

- static: Declares a member that belongs to the type itself instead of to a specific object.

- unsafe: Declares an unsafe context.

- virtual: Declares a method or an accessor whose implementation can be changed by an overriding member in a derived class.

- volatile: Indicates that a field can be modified in the program by something such as the operating system, the hardware, or a concurrently executing thread.
