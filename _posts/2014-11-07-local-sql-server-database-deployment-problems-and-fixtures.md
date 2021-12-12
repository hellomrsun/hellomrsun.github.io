---
layout: post
read_time: true
show_date: true
title:  Local SQL Server database deployment problems and fixtures
date:   2014-11-07 08:00:00 +0100
description: Local SQL Server database deployment problems and fixtures
img: posts/uncategorized/sqlserver.PNG
tags: [SQLServer]
author: SUN Jiangong
mathjax: yes
---


After encountering some problems in deploying databases to local server, here are some tips which could be helpful in the database deployment exercises.


When you deploy your databases. You can monitor the progress in "Data Tools Operations" view.

The deployment can have all the following steps:


- Step 1. Creating publish preview
- Step 2. Creating database script
- Step 3. Executing publish script on database 'Your database'.
- Step 4. Publish completed successfully



In my experience, the failure in Step 1 could happen when you generate the database script.

If you have this problem, build the project and retry.


In Step 2 you could meet a problem like : the script file could not be found.

In this case, just locate your project folder and find the file "{DB_Name}.dbmdl" and delete it. Then retry.

In other cases, if the database script is correctly generated and there is a problem, you can even execute and debug the script **{DB_Name}_{Publish_Number}.publish.sql**.


If you meet the problem at Step 3, you can click on "View Results"  to locate where the problem is.

If you can't locate the problem, just debug the generated SQL script.


I hope this post can do help to you!!!


Enjoy coding!

