---
layout: post
read_time: true
show_date: true
title:  BadImageFormatException 'Could not load file or assembly or one of its dependencies' in Visual Studio
date:   2014-11-08 08:00:00 +0100
description: BadImageFormatException Could not load file or assembly or one of its dependencies in Visual Studio
img: posts/uncategorized/windows.jpg
tags: [VisualStudio]
author: SUN Jiangong
mathjax: yes
---

If you have met this exception:

```batch
Could not load file or assembly '{Library_Name}, Version=0.0.0.0, Culture=neutral, PublicKeyToken={Token}' or one of its dependencies. Tentative de chargement d’un programme de format incorrect. 
```

It means the dll that you have referenced is not compatible with your project's build configuration likePlatform, or Platform target. 

<!--more-->

If your the reference library is 32 bit, you need to make sure your platform and platform target is **x86**.


If your the reference library is 64 bit, you can configure the platform and platform target as **Any CPU**.

Once all these information are consistent, try to rebuild and rerun the project. :)



Enjoy coding!




