---
layout: post
title: What is CLR profiler?
excerpt_separator:  <!--more-->
---

CLR Profiler is a .NET tool, developed by Microsoft, to evaluate the C# applications (.exe) performances.

<!--more-->

You could CLR profiler to view statistics like Heap statistics, Garbage Collection statistics, GC Handle Statistics etc.

<b>CLR Profiler interface:</b>

![](./../../../assets/images/CLR_Profiler/CLR_Profiler.PNG)


<b>CLR Profiler statistics report:</b>

![](./../../../assets/images/CLR_Profiler/CLR_profiler_stats.PNG)


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

![](./../../../assets/images/CLR_Profiler/StringBenchmark.PNG)


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

![](./../../../assets/images/CLR_Profiler/StringBuilderBenchmark.PNG)


