---
layout: post
title: Just4Fun - C# property access modifier usage
description: Just4Fun - C# property access modifier usage
excerpt_separator:  <!--more-->
tags: Just4Fun
canonical_url: 'https://sunjiangong.com/just-for-fun-csharp-property-access-modifier-usage/'
---


I've found some points to pay attention when revising the access modifiers for properties in CSharp.

#### 1. The access modfiers from higher to lower hierarchy are the following: public > protected internal > protected or internal > private

#### 2. A property's modifier's hierarchy must be higher than its getter and setter.

#### 3. A property's getter and setter can both have access modifier at the same time.

#### 4. A private property's getter and setter can't have a access modifier.


<!--more-->

<br />

Here are some correct access modifier usages:

![](./../../../assets/images/CsharpAccessModifier/01.png)


![](./../../../assets/images/CsharpAccessModifier/02.png)

<br />

Here are some wrong access modifier usages:

![](./../../../assets/images/CsharpAccessModifier/03.png)

<br />

I hope this post do help to you! Enjoy coding!
