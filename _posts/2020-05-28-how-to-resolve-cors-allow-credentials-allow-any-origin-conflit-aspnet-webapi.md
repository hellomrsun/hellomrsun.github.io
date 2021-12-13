---
layout: post
read_time: true
show_date: true
title:  How to resolve CORS AllowAnyOrigin and AllowCredentials conflict in ASPNET CORE Web API
date:   2020-05-28 08:00:00 +0100
description: How to resolve CORS AllowAnyOrigin and AllowCredentials conflict in ASPNET CORE Web API, ASP.NET 
img: posts/2020-05-28-CorsAllowAnyOriginCredentials/solution.PNG
tags: [CORS]
author: SUN Jiangong
---

When you implement an ASP.NET CORE Web API, you may want the API to support all clients from anywhere and enable credentials at the same time.

You need to make the **CORS** (Cross Origin Resource Sharing) configuration in your Web API.

<!--more-->

The configuration would be like this:

![](./../../../assets/img/posts/2020-05-28-CorsAllowAnyOriginCredentials/wrong.PNG)

But you'll get the following error:

```batch
System.InvalidOperationException: 'The CORS protocol does not allow specifying a wildcard (any) origin and credentials at the same time. 
Configure the CORS policy by listing individual origins if credentials needs to be supported.'
```

To resolve this, you can make the following configuration.

![](./../../../assets/img/posts/2020-05-28-CorsAllowAnyOriginCredentials/solution.PNG)

