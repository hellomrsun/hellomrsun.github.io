---
layout: post
title: SqlLocalDb Versions - Windows API call RegGetValueW returned error code
excerpt_separator:  <!--more-->
tags: Entity-Framework SqlLocalDb
canonical_url: 'https://sunjiangong.com/windows-api-call-reggetvaluew-returned-error-code/'
---

I've met this error when I check the version of SQL Server LocalDb in my machine.

```cmd
>sqllocaldb.exe versions
```

Error:

![](./../../../assets/images/SqlLocalDb/SqlLocalDb_version_windows_api_error.PNG)

<!--more-->

When I check the registry.

1. Current version

**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL13E.LOCALDB\MSSQLServer\CurrentVersion**

![](./../../../assets/images/SqlLocalDb/CurrentVersion.PNG)

2. Installed version
 
**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions**

![](./../../../assets/images/SqlLocalDb/InstalledVersion.PNG)

<br/>

The two versions are inconsistent.

When I change the installed version folder name from **"13.0"** to **"13.1"**, the problem is solved.

![](./../../../assets/images/SqlLocalDb/ChangeInstalledVersion.PNG)

<br/>

Check the SQL Local Db version again in cmd, the version is correctly displayed.

![](./../../../assets/images/SqlLocalDb/SqlLocalDb_version_ok.PNG)

