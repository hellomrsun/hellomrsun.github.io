---
layout: post
read_time: true
show_date: true
title:  User accounts in Microsoft SQL Server
date:   2013-04-25 08:00:00 +0100
description: User accounts in Microsoft SQL Server
img: posts/uncategorized/sqlserver.PNG
tags: [SqlServer]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/user-accounts-in-microsoft-sql-server.html'
---

I've made a web site prototype these days, I've found there are some useful information to share with you about some usual problems about users.

1/ How to create a user and give it rights to access a database

![](./../../../assets/img/posts/2013-04-25-ms-sql-server-user/1.png)

<!--more-->

2/ Once you have correctly created your user, but you can't login with it in SQL Server. You get error 18456.

Then you need to check if the sql server is well configured. 

These are possible reasons listed by Microsoft:

- If you are trying to connect using SQL Server Authentication, verify that SQL Server is configured in Mixed Authentication Mode.
- If you are trying to connect using SQL Server Authentication, verify that SQL Server login exists and that you have spelled it properly.
- If you are trying to connect using Windows Authentication, verify that you are properly logged into the correct domain.
- If your error indicates state 1, contact your SQL Server administrator.
- If you are trying to connect using your administrator credentials, start you application by using the Run as Administrator option. When connected, add your Windows user as an individual login.
- If the Database Engine supports contained databases, confirm that the login was not deleted after migration to a contained database user.
Well the most common correction is you activate SQL Server authentication.

![](./../../../assets/img/posts/2013-04-25-ms-sql-server-user/2.png)

3/ Sometimes you want to drop a login, but a job is associated with it.

You have to firstly get all the jobs in your DB. And then delete the job.

![](./../../../assets/img/posts/2013-04-25-ms-sql-server-user/3.png)

I hope this post do help to your daily work! Enjoy coding!
