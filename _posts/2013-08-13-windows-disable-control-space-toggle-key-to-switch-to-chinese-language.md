---
layout: post
read_time: true
show_date: true
title:  How to disable Control + Space toggle key for switching to Chinese language ?
date:   2013-08-13 08:00:00 +0100
description: How to disable Control + Space toggle key for switching to Chinese language ?
img: posts/uncategorized/windows.jpg
tags: [Windows]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-disable-control-and-space-toggle-key-to-switch-chinese-language-in-windows.html'
---

The combined key Ctrl + Space for switching from en to cn is a default settings in Windows System. As far as I know, we can't disable it in the keyboard settings in configuration pannel.

We can modify the registry to disable it.

<!--more-->

In HKEY_CURRENT_USER -> Control Panel -> Input Method -> Hot Keys 

You can choose:

00000010 for Simplified Chinese

00000070 for Traditional Chinese

I use Simplified Chinese, so I click 00000010 "folder". 

You need to 

- modify "Key Modifiers" value from 20 c0 00 00 to 00 c0 00 00. 
- modify  "Virtual Key" value from 49 00 00 00 to ff 00 00 00


The case is not sensitive.

Once you have done registry modifications, you can log off and re-logon. And you will find the problem solved.


I hope this can do help to you!