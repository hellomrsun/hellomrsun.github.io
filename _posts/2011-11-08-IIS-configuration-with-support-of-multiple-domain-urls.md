---
layout: post
read_time: true
show_date: true
title:  IIS configuration with support of multiple domain urls
date:   2011-11-08 08:00:00 +0100
description: IIS configuration with support of multiple domain urls
img: posts/uncategorized/iis.png
tags: [IIS]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/IIS-configuration-with-support-of-multiple-domain-urls.html'
---

Today I have encountered a problem, I spent 3 hours and a half for figuring it out. I need to make the application compatible with muiltiple domain urls. 


I need to get the country information when parsing the two urls: cn.xx.xxx.xxxx.com and web-cn.xx.xxx.xxxx.com
What i need is simply "cn".

<!--more-->

Here is my code : 

```csharp
//Detect country by subdomain and get first culture in Front (ex  : cn.xx.xxx.xxxx.com )
//Add possibility of detect the culture in Contrib Front ( ex : web-cn.xx.xxx.xxxx.com )
if (Request.Url.Host.IndexOf('.') == 2 || Request.Url.Host.IndexOf('.') == 6)
{
	string s = Request.Url.Host.Split('.')[0];
	string l = s.Substring(s.Length - 2);
	Culture cult = GetCulture(l).FirstOrDefault();
}
```

I have two test cases in my recette envrionment, on called Contrib, the other call Front. They hold the same codes and same configurations. But in fact it works in one case and not the other one.

With confusions and frastration during 3 hours, I've found that it's because there is a tiny difference between their configurations in IIS 6.

It's just the parameter " DefaultDoc". My application's default page is "Default.aspx". It won't work if i don't indicate it in my IIS configuration. The case not working doesn't have this parameter. 

```csharp
<IIsWebVirtualDir	
		Location ="/LM/W3SVC/98004751/root"
		AccessFlags="AccessRead | AccessWrite | AccessScript"
		AppFriendlyName="AP Contrib"
		AppIsolated="2"
		AppPoolId="AP"
		AppRoot="/LM/W3SVC/98004751/Root"
		AuthFlags="AuthAnonymous | AuthNTLM"
		DefaultDoc="Default.aspx,Default.htm,Default.asp,index.htm"
		DirBrowseFlags="EnableDirBrowsing | DirBrowseShowDate | DirBrowseShowTime | DirBrowseShowSize | 	
		DirBrowseShowExtension | DirBrowseShowLongDate | EnableDefaultDoc"
		MimeMap=".woff,application/x-woff"
		Path="G:\CONTRIB"
		ScriptMaps="">
</IIsWebVirtualDir>
```

AT LAST, it work for me. Enjoy coding!!!
