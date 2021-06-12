---
layout: post
title: .NET Profiling tools 
excerpt_separator:  <!--more-->
tags: DotNet-Profiler
canonical_url: 'https://sunjiangong.com/dotnet-profiling-tools/'
---

There are some .NET profiling tools which are quite helpful to make code benchmarks and guide you to fix the application's performance problems.

<!--more-->

Here are some of them:

### 1. DotTrace

DotTrace is a profiling tool developed by JetBrains, and it's part of ReSharper Ultimate.
I personally used it and find it very useful to locate the code issues.
You can experiment it with 10 days free trial.

Link: [DotTrace](https://www.jetbrains.com/profiler/)



### 2. CLR Profiler

CLR Profiler is a legacy tool developed by Microsoft to make application profiling up to .NET framework 4.5.

It's optimal if you want to understand how CLR run your application, especially when you compare two versions of code.

You can visualize the GC statistics, Heap statistics of the profiled application. 

The disadvantage is that it doesn't support applications developed later than .NET framework 4.5.


Link: [CLR Profiler](https://github.com/microsoftarchive/clrprofiler/releases)


### 3. BenchmarkDotNet

This is a benchmark tool developed by Microsoft since 2015. And it's quite popular in the last 2-3 years.

You can easily make benchmarks on some methods in your application.

Link: [BenchmarkDotNet](https://github.com/dotnet/BenchmarkDotNet/releases)

