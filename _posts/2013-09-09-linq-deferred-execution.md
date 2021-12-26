---
layout: post
read_time: true
show_date: true
title:  Deferred execution in LINQ
date:   2013-09-09 08:00:00 +0100
description: Deferred execution in LINQ csharp c#
img: posts/uncategorized/csharp.jpg
tags: [LINQ]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/deferred-execution-in-linq.html'
---

Deferred Execution is used in LINQ, and it means the query is not executed when declaring it; but when calling it.

If you return IQueryable or IEnumerable in your query, the query will not be executed immediately, it will be executed only when you iterate its elements.

But if you return operations on IQueryable or IEnumerable like .ToList(), Count() etc, it will be executed immediately.

<!--more-->

Let's see some examples:

```csharp
public void DifferedExecutionExample()
{
    int id = 10;
    //differed execution: when query returns IEnumerable or IQueryable
    var query = from c in Context.Customers
                where c.CustomerId > id
                select c;
    id = 20; //this value is finally used because it's the latest value
    Console.WriteLine("Query result:");
    //return customer names whose id is larger than 20
    foreach (var customer in query)
        Console.WriteLine(customer.CustomerName);
}

public void ImmediateExecutionExample()
{
    int id2 = 10;
    //immediate execution: when query doesn't return IEnumerable or IQueryable
    var query2 = (from c in Context.Customers
                    where c.CustomerId > id2
                    select c).ToList();
    id2 = 20; //this value is not used in this case
    Console.WriteLine("Query2 result:");
    //return customer names whose id is large than 10
    foreach (var customer in query2)
        Console.WriteLine(customer.CustomerName);
}
```

I hope this article can do help to you! Enjoy coding!
