---
layout: post
title: Design patterns - Introduction to configuration wrapper
description: Design patterns - Introduction to configuration wrapper
excerpt_separator:  <!--more-->
tags: Design-Patterns
canonical_url: 'https://sunjiangong.com/design-patterns-introduction-to-configuration-wrapper/'
---

In your applications, you are certainly using the configuration sections like appSettings for custom configurations, connectionStrings for database binding and other sections like WCF bindings, etc.

To make your application more flexible for unit testing, you could use a configuration wrapper to control the access to the configuration file.

You can create an interface to expose some methods to access different configurations.

<!--more-->

This is two methods to retrieve the appSettings and connectionStrings by the configuration key.

```csharp
public interface IConfigurationReader
{
    string GetAppSettings(string key);

    string GetConnectionString(string key);
}
```

Here are their implementation.

```csharp
public class ConfigurationReader : IConfigurationReader
{
    public string GetAppSettings(string key)
    {
        return ConfigurationManager.AppSettings[key];
    }

    public string GetConnectionString(string key)
    {
        return ConfigurationManager.ConnectionStrings[key].ConnectionString;
    }
}
```

You can register the interface and its implementation with dependency injection pattern using UnityContainer.

IUnityContainer container = new UnityContainer();

```csharp
//register interface and its implementation
container.RegisterType<IConfigurationReader, ConfigurationReader>();
```

Resolve the interface and use the class to access the configuration value.

```csharp
//resolve the interface
var configurationReader = container.Resolve<IConfigurationReader>();

//access GetAppSettings method to get the value
var value = configurationReader.GetAppSettings("hello");
Console.WriteLine(value);
```


You can even centralize the configuration keys in a static class to facilitate the configuration key management.

I hope you find this article useful! Thanks.