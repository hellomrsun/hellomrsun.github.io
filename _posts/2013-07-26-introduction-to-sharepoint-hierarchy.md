---
layout: post
read_time: true
show_date: true
title:  Introduction to SharePoint hierarchy
date:   2013-07-26 05:00:00 +0100
description: Introduction to SharePoint hierarchy
img: posts/uncategorized/sharepoint.png
tags: [SharePoint]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/introduction-to-SharePoint-hierarchy.html'
---


I've worked in a SharePoint 2010 project to build an intranet. Based on this experience, I want to introduce you the basics of SP.


The top of the hierarchy is SPFarm, it's static. You can access SPFarm using SPFarm.Local

![](./../../../assets/img/posts/2013-07-26-sharepoint-hierarchy/01.png)

<!--more-->

SPFarm contains SPService.

![](./../../../assets/img/posts/2013-07-26-sharepoint-hierarchy/02.png)

Then, SPWebApplication is relavant to IIS Website. 

![](./../../../assets/img/posts/2013-07-26-sharepoint-hierarchy/03.png)

SPSite is relavant to site collections.

![](./../../../assets/img/posts/2013-07-26-sharepoint-hierarchy/04.png)

![](./../../../assets/img/posts/2013-07-26-sharepoint-hierarchy/05.png)

SPWeb means SharePoint sites.

![](./../../../assets/img/posts/2013-07-26-sharepoint-hierarchy/06.png)

![](./../../../assets/img/posts/2013-07-26-sharepoint-hierarchy/07.png)

The hierarchy of SharePoint is:

![](./../../../assets/img/posts/2013-07-26-sharepoint-hierarchy/08.png)