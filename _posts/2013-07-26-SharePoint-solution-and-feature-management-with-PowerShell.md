---
layout: post
read_time: true
show_date: true
title:   SharePoint solution and feature management with powershell
date:   2013-07-26 07:00:00 +0100
description: SharePoint solution and feature management with powershell
img: posts/uncategorized/sharepoint.png
tags: [SharePoint]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/SharePoint-solution-and-feature-management-with-powershell.html'
---


I want to introduce SharePoint solution and feature management using powershell.


Before we install a SPSolution, we need to put it on the Farm.

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/01.png)

<!--more-->

Once added, we can install it.

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/02.png)

If you have some modifications on your solution, you can update it.

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/03.png)

If you don't want the solution, you can uninstall it on the farm.

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/04.png)

If you want to remove the solution from the farm, you can do this.

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/05.png)

If you want to see all the installed solutions.

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/06.png)

If you want to see a specific solution

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/07.png)

Here are the basic solution management with powershell.

Now, let's see how to manage features.


We can enable a feature

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/08.png)

And disable it.

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/09.png)

And check all the features on a site

![](./../../../assets/img/posts/2013-07-26-sharepoint-solution/10.png)

So, we are arrived at the end, I hope you enjoy this!