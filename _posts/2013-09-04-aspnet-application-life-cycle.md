---
layout: post
title: ASP.NET page lifecycle in IIS
description: ASP.NET page lifecycle in IIS
excerpt_separator:  <!--more-->
tags: IIS
canonical_url: 'https://sunjiangong.com/aspnet-page-lifecycle-in-iis/'
---


Today, I want to share the knowledge about IIS, Application Life Cycle, request handling and so on.


ASP.NET web sites are developed with Web Forms, MVC, Web Pages and hosted in Internet Information Server (IIS). 

<!--more-->

When  there is a page request, for example: http://www.example.com/index.aspx, IIS will use its Internet Server Application Programming Interface(ISAPI)

IIS will decide that the request will be treated by aspx(active server pages), ashx(active server handlers), ascx(active server controls) or asmx(active server methods).

If you want to treat any custom type of files, you need to create a custom handler and register it to IIS. 


The request handling process are Request -> IIS -> ISAPI -> Application Domain -> Http Runtime -> HttpContext -> MHPM(HttpModule, HttpHandler, Page life, HttpModule)


ASP.NET Web Forms Page lifecycle is different from ASP.NET MVC.

In Web Forms, page lifecycle model is the following:

![](./../../../assets/images/AspNetPageLifeCycle/webforms_lifecycle.png)

ViewState and PostBack data are loaded in Page_PreLoad event. And Validate and Event are after Page_Load event.


Whereas in ASP.NET MVC it is:

![](./../../../assets/images/AspNetPageLifeCycle/mvc_lifecycle.png)

There is not any code behind for pages in MVC. So, the page life cycle is totoally different.

I hope you enjoy this article. 

