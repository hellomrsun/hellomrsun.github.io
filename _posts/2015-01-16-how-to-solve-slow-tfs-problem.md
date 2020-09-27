---
layout: post
title: How to solve slow TFS response problem in Visual Studio?
description: How to solve slow TFS response problem in Visual Studio?
excerpt_separator:  <!--more-->
tags: TFS
canonical_url: 'https://sunjiangong.com/how-to-solve-slow-TFS-response-problem-in-visual-studio/'
---


Assume that your environment is Visual studio and TFS server. 

At one day, when you make modifications in your solution, such as, create a new file, or update a file name. Then visual studio takes a long time to respond. 

You may meet the TFS response problem.

<!--more-->

In this case, you may try to restart visual studio or your system or make some other tries. But it won't work.

You need to **refresh** your workspace to solve this problem, which means delete the entire workspace and re-make the mapping. 

But you should backup your current modifications in the solution by shelve them.


Hope this can do help!