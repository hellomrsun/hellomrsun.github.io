---
layout: post
title: Introduction to dependency injection with unity container
description: Introduction to dependency injection with unity container
excerpt_separator:  <!--more-->
tags: Design-Patterns
canonical_url: 'https://sunjiangong.com/introduction-to-dependency-injection-with-unity-container/'
---


This article is just a simple introduction to unityContainer.

If you have already used unityContainer as a dependency injection or IoC (Inversion of control) library, this article is not for you.

As you know, dependency injection is a design pattern to prevent the code coupling.

<!--more-->

For example, you access class CA’s method MA in several places in your application. If one day you need to use class CB instead of class CA. You need to replace all the code referencing class CA with class CB.

But if you use dependency injection, you just need to register the interface and its implementation class once. You can resolve the interface when you need to access method CA.

Here is an sample usage of unityContainer:

Firstly, create an instance of UnityContainer.

```csharp
//register interface and its implementation
IUnityContainer container = new UnityContainer();
```

Register the interface and its implementation class.

```csharp
container.RegisterType<IConfigurationReader, ConfigurationReader>();
```

Resolve the interface:

```csharp
var configurationReader = container.Resolve<IConfigurationReader>();
```

Access to method :

```csharp
var value = configurationReader.GetAppSettings("hello");
```

In this way, you won’t need to create any instance of a specific class. The code is more maintainable.

I hope you find this article helpful!