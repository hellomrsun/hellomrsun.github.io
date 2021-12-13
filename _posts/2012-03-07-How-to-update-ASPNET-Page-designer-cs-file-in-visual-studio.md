---
layout: post
read_time: true
show_date: true
title:  How to update ASP.NET Page's .designer.cs file in visual studio
date:   2012-03-07 08:00:00 +0100
description: .NET, Dotnet, C#, Csharp, ASP.NET, designer.cs, ASP-NET, Visual Studio
img: posts/uncategorized/Visual-Studio.png
tags: [ASPNET, Visual-Studio]
author: SUN Jiangong
mathjax: yes
---

I want to add repeater, litteral or register user control in ASP.NET pages. Sometimes the page's ".designer.cs" file doesn't update immediately.

I've tried to close the solution, delete project temporary files in "C:\Windows\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files", and then reopen the solution.

While it doesn't work at most of the time. It's quite frustrating.

<!--more-->
<br />

**Solution:**

If you can't update the page.designer.cs file correctly even if you have tried several times close/open solution, add/delete controls etc. You can try to regenerate your .designer.cs file.

For example, you have a page Homepage.aspx. 

The structure should be:

- Homepage.aspx
  - Homepage.aspx.cs
  - -Homepage.aspx.designer.cs

<br />

What you should do:

1) Delete your "Homepage.aspx.designer.cs"

2) Right click on "Homepage.aspx", then click "Convert to Web Application", the new designer file will be generated.

3) Close and reopen solution

4) Click "Show all files" and include new generated designer file

<br />

At last, you will find all the controls you need in designer file.