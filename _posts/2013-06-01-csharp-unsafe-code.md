---
layout: post
read_time: true
show_date: true
title:  C# unsafe code
date:   2013-06-01 07:00:00 +0100
description: C# unsafe code
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/csharp-unsafe-code.html'
---

To maintain type safety and security, C# does not support pointer arithmetic, by default. However, by using the unsafe keyword, you can define an unsafe context in which pointers can be used. 

In the common language runtime (CLR), unsafe code is referred to as unverifiable code. Unsafe code in C# is not necessarily dangerous; it is just code whose safety cannot be verified by the CLR. The CLR will therefore only execute unsafe code if it is in a fully trusted assembly. If you use unsafe code, it is your responsibility to ensure that your code does not introduce security risks or pointer errors.

<!--more-->

Unsafe code must be compiled by csharp compiler with keyword "/unsafe"

```csharp
csc /unsafe class.cs
```

There are 3 types in CSharp language, which are Value type, Reference type, Pointer type. 

Pointer types can only be used in unsafe mode.
