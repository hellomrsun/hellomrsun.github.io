---
layout: post
read_time: true
show_date: true
title:  Just4Fun CSharp - property access modifier usage
date:   2014-12-28 08:00:00 +0100
description: Just4Fun C# property access modifier usage
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/just-for-fun-csharp-property-acess-modifier-usage.html'
mathjax: yes
redirect_from:
  - /2014/12/28/just4fun-csharp-property-acess-modifier-usage.html
---


I've found some points to pay attention when revising the access modifiers for properties in CSharp.

#### 1. The access modfiers from higher to lower hierarchy are the following: public > protected internal > protected or internal > private

#### 2. A property's modifier's hierarchy must be higher than its getter and setter.

<!--more-->

#### 3. A property's getter and setter can both have access modifier at the same time.

#### 4. A private property's getter and setter can't have a access modifier.

<br />

Here are some correct access modifier usages:

![](./../../../assets/img/posts/2014-12-28-CsharpAccessModifier/01.png)


![](./../../../assets/img/posts/2014-12-28-CsharpAccessModifier/02.png)

<br />

Here are some wrong access modifier usages:

![](./../../../assets/img/posts/2014-12-28-CsharpAccessModifier/03.png)

<br />

I hope this post do help to you! Enjoy coding!
