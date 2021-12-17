---
layout: post
read_time: true
show_date: true
title:  Type Inference and usage of var in C#
date:   2013-01-25 08:00:00 +0100
description: Type Inference and usage of var in C#
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/type-inference-and-usage-of-var-in-csharp.html'
mathjax: yes
redirect_from:
  - /2013/09/05/type-inferrence-in-csharp.html
---


Type Inference a concept of C# 3 that is used with keyword var, which lets the compiler decide the object type.

It's mainly used with anonymous types and LINQ when you manipulate different types of data like XML, SQL, Entities and Objects.

If you have to treat some data which is used only once, and in a local scope, you don't have to create a new type for it. You can just use anonymous type. In case of modification, you just need to modify your data directly.

<!--more-->

For example:

```csharp
var belle = new {Name = "Belle", Age = "15", Sex = "Female"};
```

As to the usage of data source, you just need to handle part of the data type in most cases. And this can reduce the network traffic and server charges.
For example:

```csharp
var ienums = from c in customers
             select new { Name = c.CustomerFirstName, Id = c.CustomerId };
```

In more complicated cases, it's not recommended to use Explicit types than anonymous types too.

Next, I'll talk about the usage of var. 

If you and your collegues can easily understand what type the object is, you can use explicit type or var. 

If you are initializing data with declaration and the type is complicated, it's recommended to use var for preventing bad readability and distraction of attention.

If you are treating data from different data sources and it's used once, you can use var. If it's used widely in an application, you can convert to a specific type.

If you are using anonymous type, you need var.

If you are in other cases, it's recommended to use explicit type.


I hope this post can do help to your daily work! Enjoy coding!