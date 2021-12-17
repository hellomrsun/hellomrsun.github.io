---
layout: post
read_time: true
show_date: true
title:  How to solve 'You have been logged on with a temporary profile error' in Windows?
date:   2014-10-21 08:00:00 +0100
description: How to solve You have been logged on with a temporary profile error in Windows
img: posts/uncategorized/windows.jpg 
tags: [Windows]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-solve-you-have-been-logged-on-with-a-temporary-profile-error-in-windows.html'
mathjax: yes
redirect_from:
  - /2014/10/21/how-to-solve-you-have-been-logged-on-with-a-temporary-profile.html
---


I've encountered a problem in one server, which is : Every time I login into the server, it creates a new temporary user profile for my account.


Here is the error message:

```batch
You have been logged on with a temporary profile. You cannot access your files and files created in this profile will be deleted when you log off. To fix this, log off and try logging on later. Please see the event log for details or contact your system administrator.
```

<!--more-->

You can check the registry to see if the account have a or several temporary profiles with the following path.

**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList**

By check the profiles list, you may find there are two profiles using similar names.

For example, a profile called "S-1-5-82" and another profile called "S-1-5-82.bak".

If you check further, you will find the .bak profile's "ProfileImagePath" value is your account, and the currently used profile's "ProfileImagePath" is a temporary profile you're using right now.


To solve this problem, you can just rename the profile "S-1-5-82" to "S-1-5-82.tmp", and revert "S-1-5-82.bak" to "S-1-5-82".

In this way, the correct profile is used. 

Then restart the server, and the problem should be fixed.


<br/>

References:

http://www.techsupportall.com/how-to-fix-temporary-profile-in-windows-7/

http://support.microsoft.com/kb/947242
