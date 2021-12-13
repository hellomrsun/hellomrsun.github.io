---
layout: post
read_time: true
show_date: true
title:  C# - Extension method usage
date:   2013-09-07 08:00:00 +0100
description: C# - Extension method usage
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
mathjax: yes
---


Extension methods enable you to "add" methods to existing types without creating a new derived type, recompiling, or otherwise modifying the original type. 

Extension methods are a special kind of static method, but they are called as if they were instance methods on the extended type.

The most common extension methods are in LINQ; Linq provides two classes: Enumerable and Queryable. And their extensions methods operate on IEnumerable<T> and IQueryable<T>.

Extension methods are static methods who reside in static utility classes.

<!--more-->

For example:

```csharp
public static bool IsNull(this object x)
{
    return x == null;
}
public static bool IsNullOrEmpty(this object text)
{
    return text == null || (string)text == "";
}
public static IEnumerable<int> GetOddMembers(this List<int> list)
{
    return list.Where(x => x%2 != 0);
}
```

Usage:

```csharp
object y = null;
Console.WriteLine(y.IsNull()); //True
y = new object();
Console.WriteLine(y.IsNull()); //False

object s = null;
Console.WriteLine(s.IsNullOrEmpty()); //True
s = string.Empty;
Console.WriteLine(s.IsNullOrEmpty()); //True
s = "hello";
Console.WriteLine(s.IsNullOrEmpty()); //False

Console.WriteLine(IsObjectNull.IsNullOrEmpty(null)); //True

List<int> list = new List<int>() {1, 2, 5, 7, 12};
var oddMembers = list.GetOddMembers();
foreach (var oddMember in oddMembers)
{
    Console.WriteLine(oddMember); //1 5 7
}
```            

I Hope this can do help to you! 

Enjoy coding!
