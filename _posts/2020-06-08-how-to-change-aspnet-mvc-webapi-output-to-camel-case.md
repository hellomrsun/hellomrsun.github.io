---
layout: post
read_time: true
show_date: true
title:  How to change ASP NET MVC Web API output to camelCase
date:   2020-06-08 08:00:00 +0100
description: How to change ASP NET MVC Web API output to camelCase
img: posts/2020-06-08-aspnet-webapi/webapi.png
tags: [WebApi]
author: SUN Jiangong
mathjax: yes
---

Unlike ASP.NET CORE Web API, ASP.NET MVC Web API's will not serialize the output in camelCase.

camelCase example: 

```csharp
firstName
lastName
```

PascalCase example:

```csharp
FirstName
LastName
```

<!--more-->

So you may encounter the difference when you convert your API from ASP.NET MVC Web API to ASP.NET CORE Web API or vice versa.

Don't panic!

In the case that you need to enable the camelCase in ASP.NET MVC Web API, you can change the json formatter settings in the startup configuration, as following:

```csharp
public void Configuration(IAppBuilder app){
    var config = new HttpConfiguration;
    config.Formatters.Remove(config.Formatter.XmlFormatter);
    config.Formatters.Add(config.Formatter.JsonFormatter);
    config.Formatters.JsonFormatter.SerializerSettings.ContractResolver = new CamelCasePropertyNamesContractResolver();
    config.Formatters.JsonFormatter.UseDataContractJsonSerializer = false;
}
```

