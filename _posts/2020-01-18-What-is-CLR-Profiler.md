---
layout: post
read_time: true
show_date: true
title:  What is CLR profiler?
date:   2020-01-18 08:00:00 +0100
description: What is CLR profiler? 
img: posts/2020-01-18-ClrProfiler/StringBenchmark.png
tags: [Profiler]
author: SUN Jiangong
mathjax: yes
redirect_from:
  - /2020/01/18/What-is-CLR-Profiler.html
---

CLR Profiler is a .NET tool, developed by Microsoft, to evaluate the C# applications (.exe) performances.

You could CLR profiler to view statistics like Heap statistics, Garbage Collection statistics, GC Handle Statistics etc.

<b>CLR Profiler interface:</b>

![](./../../../assets/img/posts/2020-01-18-ClrProfiler/CLR_Profiler.PNG)

<!--more-->
<br/>

For example, I can compare the differences between String concatenation and StringBuilder appending in a console application.

<br />

<b>String concatenation:</b>

```csharp
public class StringBenchmark
{
    public void Build()
    {
        var text = "Hello"; ;
        for (var i = 0; i < 20000; i++)
        {
            text += "World";
        }
    }
}
```

Result:

![](./../../../assets/img/posts/2020-01-18-ClrProfiler/StringBenchmark.PNG)


<br/>


<b>StringBuilder appending:</b>
```csharp
public class StringBuilderBenchmark
{
    public void Build()
    {
        var builder = new StringBuilder().Append("Hello");
        for (var i = 0; i < 20000; i++)
        {
            builder.Append("World");
        }
    }
}
```

Result:

![](./../../../assets/img/posts/2020-01-18-ClrProfiler/StringBuilderBenchmark.PNG)


You can compare the differences in the two reports.

<br/>

[Download CLR Profiler](https://github.com/microsoftarchive/clrprofiler/releases)