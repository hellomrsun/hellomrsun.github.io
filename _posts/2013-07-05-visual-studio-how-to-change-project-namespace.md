---
layout: post
read_time: true
show_date: true
title:  Visual Studio Tips - How to change project namespace
date:   2013-07-05 06:00:00 +0100
description: Visual Studio Tips - How to change project namespace
img: posts/uncategorized/Visual-Studio.png
tags: [VisualStudio]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-change-project-namespace-in-visual-studio.html'
---

If you want to modify a project's namespace and its physical container name, here are some steps to do:


In Visual Studio:

- Change the namespace in the code

- Change the namespace for the project

- Go to project properties, and modify the assembly name and default namespace

<!--more-->

In your system:

- Locate the solution file .sln and modify the project path.

![](./../../../assets/img/posts/2013-07-05-project-namespace/01.png)

Now reload your solution, it works!


I hope this article can do help to you! Enjoy coding!