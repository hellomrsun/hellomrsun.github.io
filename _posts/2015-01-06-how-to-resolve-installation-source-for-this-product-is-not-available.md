---
layout: post
title: How to solve "The installation source for this product is not available" error?
description: How to solve "The installation source for this product is not available" error?
excerpt_separator:  <!--more-->
tags: TFS
canonical_url: 'https://sunjiangong.com/how-to-solve-installation-source-for-this-product-is-not-available/'
---


When you develop your enterprise application and deploy your application as a window service, you may encounter the following problem : 

```batch
The installation source for this product is not available. Verify that the source exists and that you can access it.
```

<!--more-->

In this case, you can not install a new version of windows service because the installed service is corrupted and exists in the system.

The installed service should be existed in "Administration Tools -> Services" and "Control panel -> Programs" 

And to deploy or install a new version of service, you need to remove the two services.

Here are two steps to make it:

#### 1. Use windows "Fix It" tool to solve the registry corruption problem

http://support.microsoft.com/kb/971187

It will remove the installed programs.

#### 2. Use "Service Control" command to delete the service 


```batch
> sc delete {serviceName}
```

http://technet.microsoft.com/en-us/library/bb490995.aspx

It will remove the installed service.