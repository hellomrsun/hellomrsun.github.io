---
layout: post
read_time: true
show_date: true
title:  SQL Server installation - Could not load file or assembly 'System, Version=4.0.0.0'
date:   2013-06-28 07:00:00 +0100
description: SQL Server installation - Could not load file or assembly 'System, Version=4.0.0.0'
img: posts/uncategorized/sqlserver.PNG
tags: [SqlServer]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/sql-server-2008-installaion-error-could-not-load-file-or-assembly-system.html'
---

The error:

Could not load file or assembly 'System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The system cannot find the file specified. 

C:\Users\[UserName]\AppData\Local\Microsoft_Corporation\LandingPage.exe_StrongName_ryspccglaxmt4nhllj5z3thycltsvyyx\10.0.0.0\user.config

Reason:

A SQL Server 2008 installation is interrupted.


Solution:

Delete the folder: C:\Users\[UserName]\AppData\Local\Microsoft_Corporation
