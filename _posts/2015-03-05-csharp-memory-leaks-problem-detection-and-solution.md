---
layout: post
# title: Memory leaks problem detection and solution in C#
# description: Memory leaks problem detection and solution in C#
# excerpt_separator:  <!--more-->
# tags: Profiler
# canonical_url: 'https://sunjiangong.com/csharp-memory-leaks-problem-detection-and-solution/'
read_time: true
show_date: true
title:  Memory leaks problem detection and solution in C#
date:   2015-03-05 08:00:00 +0100
description: Memory leaks problem detection and solution in C#
img: posts/2015-03-05-MemoryLeaks/02.png
tags: [Profiler]
author: SUN Jiangong
# github:  hellomrsun
mathjax: yes
---


Out of memory exception happens when server doesn’t have enough memory to run the application.

This often happens when you are dealing with external resources, such as consuming Interop libraries, treating files, streams, etc.

Memory is a limited resource, it’s easy to be run out of. So, you should be careful when you are working with external resources in your application development.

<!--more-->

There are some good memory profilers in the market.

I’ve listed two profilers I’ve used. They are both very easy to use. You can even try them for a limited period.

- DotTrace
- Ants Memory Profiler


Here are some screenshots of one snapshot in Ants memory profiler.

You could see the memory usage progress with time.


You could easily see the memory usage with Heap generation 1, generation 2, Large object heap, Unused memory allocated to .NET, Unmanaged memories.

![](./../../../assets/img/posts/2015-03-05-MemoryLeaks/01.png)


Then you could investigate which instance of class is used, how much times it’s been used, how many memory it has occupied, etc.

![](./../../../assets/img/posts/2015-03-05-MemoryLeaks/02.png)


The best practice to consume an external data source is using “using” statement. Everything you get in external services will be disposed.

```csharp
using (var service = _serviceAdapter.Configure())
{
    var data = _serviceAdapter.RetrieveData(parameters);
}
```

If you need to use the retrieved data in several places in your application. You can convert it to a DTO object, so the code becomes managed.

```csharp
DataDto dataDto = new DataDto();
using (var service = _serviceAdapter.Configure())
{
    var data = _serviceAdapter.RetrieveData(parameters);
    dtoData = ConvertToDto(data);
}
```

In this way you can use dtoData wherever you like.
After the object’s usage, the data will be collected by GC later.

You can translate the previous code into :

```csharp
Service service = new Service();
Data data = new Data();
try
{
    service = _serviceAdapter.Configure();
    data = _serviceAdapter.RetrieveData(parameters);
    dtoData = ConvertToDto(data);
}
finally
{
    service.Dispose();
    data.Dispose();
}
```

If you want to ensure that all exceptions will be caught. You can do something like this:

```csharp
Service service = new Service();
Data data = new Data();
try
{
    service = _serviceAdapter.Configure();
    data = _serviceAdapter.RetrieveData(parameters);
    dtoData = ConvertToDto(data);
}
catch(Exception ex)
{
    Logger.LogError(ex.Message + ex.StackTrace);
}
finally
{
    service.Dispose();
    data.Dispose();
}
```

I hope you find this articles helpful!