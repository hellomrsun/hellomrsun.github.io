---
layout: post
title: How to resolve CORS AllowAnyOrigin and AllowCredentials conflict in ASPNET CORE Web API
excerpt_separator:  <!--more-->
tags: CORS
canonical_url: 'https://sunjiangong.com/how-to-resolve-cors-allow-credentials-allow-any-origin-conflit-aspnet-webapi/'
---

When you implement an ASP.NET CORE Web API, you may want the API to support all clients from anywhere and enable credentials at the same time.

You need to make the **CORS** (Cross Origin Resource Sharing) configuration in your Web API.

<!--more-->

The configuration would be like this:

![](./../../../assets/images/CorsAllowAnyOriginCredentials/wrong.PNG)

But you'll get the following error:

```batch
System.InvalidOperationException: 'The CORS protocol does not allow specifying a wildcard (any) origin and credentials at the same time. 
Configure the CORS policy by listing individual origins if credentials needs to be supported.'
```

To resolve this, you can make the following configuration.

![](./../../../assets/images/CorsAllowAnyOriginCredentials/solution.PNG)

