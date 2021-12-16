---
layout: post
read_time: true
show_date: true
title:  SqlLocalDb Versions - Windows API call RegGetValueW returned error code
date:   2020-03-28 08:00:00 +0100
description: SqlLocalDb Versions - Windows API call RegGetValueW returned error code
img: posts/2020-03-28-SqlLocalDb/InstalledVersion.PNG
tags: [EntityFramework, SQLServer]
author: SUN Jiangong
mathjax: yes
redirect_from:
  - /2020/03/28/SqlLocalDb_version.html
---

I've met this error when I check the version of SQL Server LocalDb in my machine.

```cmd
>sqllocaldb.exe versions
```

Error:

![](./../../../assets/img/posts/2020-03-28-SqlLocalDb/SqlLocalDb_version_windows_api_error.PNG)

<!--more-->

When I check the registry.

1. Current version

**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL13E.LOCALDB\MSSQLServer\CurrentVersion**

![](./../../../assets/img/posts/2020-03-28-SqlLocalDb/CurrentVersion.PNG)

2. Installed version
 
**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions**

![](./../../../assets/img/posts/2020-03-28-SqlLocalDb/InstalledVersion.PNG)

<br/>

The two versions are inconsistent.

When I change the installed version folder name from **"13.0"** to **"13.1"**, the problem is solved.

![](./../../../assets/img/posts/2020-03-28-SqlLocalDb/ChangeInstalledVersion.PNG)

<br/>

Check the SQL Local Db version again in cmd, the version is correctly displayed.

![](./../../../assets/img/posts/2020-03-28-SqlLocalDb/SqlLocalDb_version_ok.PNG)

