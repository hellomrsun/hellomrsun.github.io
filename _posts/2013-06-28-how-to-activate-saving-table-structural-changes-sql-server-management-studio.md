---
layout: post
read_time: true
show_date: true
title:  SQL Server Management Studio Tips - How to activate saving table modifications
date:   2013-06-28 08:00:00 +0100
description: SQL Server Management Studio Tips - How to activate saving table modifications
img: posts/uncategorized/sqlserver.PNG
tags: [SqlServer]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-activate-saving-table-structural-changes-in-sql-server-management-studio.html'
---

Once you have created a table using Sql Server Management Studio, you have done changes the table structure, you want to save it.

But SSMS doesn't allow you to do so.

You need to modify the configuration in Tools -> Options -> Designers and uncheck "Prevent saving changes that require table re-creation".

![](./../../../assets/img/posts/2013-06-28-ssms/01.png)


I hope this post can do help to you!
