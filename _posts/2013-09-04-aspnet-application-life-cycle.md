---
layout: post
read_time: true
show_date: true
title:  ASP.NET page lifecycle in IIS
date:   2013-09-04 08:00:00 +0100
description: ASP.NET page lifecycle in IIS
img: posts/uncategorized/iis.png
tags: [IIS]
author: SUN Jiangong
mathjax: yes
---


Today, I want to share the knowledge about IIS, Application Life Cycle, request handling and so on.


ASP.NET web sites are developed with Web Forms, MVC, Web Pages and hosted in Internet Information Server (IIS). 

When  there is a page request, for example: http://www.example.com/index.aspx, IIS will use its Internet Server Application Programming Interface(ISAPI)

IIS will decide that the request will be treated by aspx(active server pages), ashx(active server handlers), ascx(active server controls) or asmx(active server methods).

If you want to treat any custom type of files, you need to create a custom handler and register it to IIS. 

<!--more-->

The request handling process are Request -> IIS -> ISAPI -> Application Domain -> Http Runtime -> HttpContext -> MHPM(HttpModule, HttpHandler, Page life, HttpModule)


ASP.NET Web Forms Page lifecycle is different from ASP.NET MVC.

In Web Forms, page lifecycle model is the following:

![](./../../../assets/img/posts/2013-09-04-AspNetPageLifeCycle/webforms_lifecycle.png)

ViewState and PostBack data are loaded in Page_PreLoad event. And Validate and Event are after Page_Load event.


Whereas in ASP.NET MVC it is:

![](./../../../assets/img/posts/2013-09-04-AspNetPageLifeCycle/mvc_lifecycle.png)

There is not any code behind for pages in MVC. So, the page life cycle is totoally different.

I hope you enjoy this article. 

