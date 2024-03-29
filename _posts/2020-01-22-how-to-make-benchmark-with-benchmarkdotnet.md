---
layout: post
read_time: true
show_date: true
title:  How to make benchmark with BenchmarkDotNet?
date:   2020-01-22 07:00:00 +0100
description: How to make benchmark with BenchmarkDotNet? Microsoft, CLR Profiler, BenchmarkDotnet
img: posts/2020-01-22-BenchmarkDotNet/nuget.PNG
tags: [DotNet, Profiler, Benchmark]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-make-benchmark-with-benchmarkdotnet.html'
---

BenchmarkDotNet is a .NET benchmark tool, developed by Microsoft.

You can install BenchmarkDotNet Nuget package in your project.

![](./../../../assets/img/posts/2020-01-22-BenchmarkDotNet/nuget.PNG)

<!--more-->

Here I will benchmark the same codes in the post [CLR Profiler post](https://hellomrsun.github.io/2020/01/18/What-is-CLR-Profiler.html)

<br/>

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

<br />

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

<br/>

I want to run 1000 times the code with RunStrategy: CodeStart.

```csharp
[SimpleJob(RunStrategy.ColdStart, targetCount: 1000)]
public class BenchmarkStringVsStringBuilder
{
    private readonly StringBenchmark _sb = new StringBenchmark();
    private readonly StringBuilderBenchmark _sbb = new StringBuilderBenchmark();

    [Benchmark]
    public void StringBenchmark() => _sb.Build();

    [Benchmark]
    public void StringBuilderBenchmark() => _sbb.Build();
}
```

<br/>

Run benchmark job:


```csharp
class Program
{
    static void Main(string[] args)
    {
        BenchmarkRunner.Run<BenchmarkStringVsStringBuilder>();
    }
}
```

<br/>

There are 3 run strategies:
  
  Throughput mode: Perfect for microbenchmarking
  
  ColdStart: Perfect for startup time evaluation. A mode without overhead evaluating and warmup, with single invocation.
  
  Monitoring: Perfect for macrobenchmarks without a steady state with high variance. A mode without overhead evaluating, with several target iterations.

<br/>

<b>The Benchmark result with ColdStart strategy:</b>

IterationCount=1000  RunStrategy=ColdStart  

```
|                 Method |         Mean |       Error |       StdDev |       Median |
|----------------------- |-------------:|------------:|-------------:|-------------:|
|        StringBenchmark | 447,726.2 us | 7,758.70 us | 74,342.43 us | 427,711.8 us |
| StringBuilderBenchmark |     227.4 us |     6.81 us |     65.29 us |     196.6 us |
```

<br/>


<b>The Benchmark result with Throughput strategy:</b>

IterationCount=1000  RunStrategy=Throughput  

```
|                 Method |         Mean |       Error |       StdDev |       Median |
|----------------------- |-------------:|------------:|-------------:|-------------:|
|        StringBenchmark | 441,113.3 us | 3,311.90 us | 30,095.62 us | 438,109.2 us |
| StringBuilderBenchmark |     242.8 us |     1.69 us |     15.71 us |     241.6 us |
```
<br/>

IterationCount=1000  RunStrategy=Monitoring  

```
|                 Method |         Mean |        Error |        StdDev |       Median |
|----------------------- |-------------:|-------------:|--------------:|-------------:|
|        StringBenchmark | 497,548.0 us | 13,720.76 us | 131,469.69 us | 461,937.8 us |
| StringBuilderBenchmark |     203.1 us |      4.55 us |      43.55 us |     180.6 us |
```

See more about [BenchmarkDotNet](https://benchmarkdotnet.org)
