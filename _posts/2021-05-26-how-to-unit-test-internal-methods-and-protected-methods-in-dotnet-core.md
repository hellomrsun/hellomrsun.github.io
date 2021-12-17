---
layout: post
read_time: true
show_date: true
title:  How to create unit tests on internal methods and protected methods in .net core?
date:   2021-05-26 08:00:00 +0100
description: How to create unit tests on internal methods and protected methods in dotnet core?
img: posts/2021-05-26-InternalProtectedMethodsUnitTest/1_set_internal_visible_in_class.PNG 
tags: [DotNetCore, DotNet, UnitTest]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-unit-test-internal-methods-and-protected-methods-in-dotnet-core.html'
redirect_from:
  - /2021/05/26/unit-test-internal-and-protected-methods.html
---

You'll inevitablly write unit tests or integration tests for internal methods and protected methods in your .net project.

Here are some techniques you can use.

To test internal methods in projects developed in .NET Framework, you need add the following code in the AssemblyInfo.cs of the target target, then all its internal methods are visible to the tests project.

```csharp
[assembly: InternalsVisibleTo("AssemblyName.Test")]
```

<!--more-->

<br/>

or with public signed key:

```csharp
[assembly: InternalsVisibleTo("AssemblyName.Test, PublicKey=0024000004800000940000000602000000240000525341310004000001000100b5fc90e7027f67871e773a8fde8938c81dd402ba65b9201d60593e96c492651e889cc13f1415ebb53fac1131ae0bd333c5ee6021672d9718ea31a8aebd0da0072f25d87dba6fc90ffd598ed4da35e44c398c454307e8e33b8426143daec9f596836f97c8f74750e5975c64e2189f45def46b2a2b1247adc3652bf5c308055da9")]
```

<br/>

But there is no AssemblyInfo.cs in .NET Core **by default**, unless if you want to keep them explicitly.

All the assembly related information are stored in the project file (.csproj) in dotnet core.

For example:
```csharp
<PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <Authors>SUN Jiangong</Authors>
    <Company>SUN Jiangong</Company>
    <Description>This is the description</Description>
    <Copyright>@SUN Jiangong</Copyright>
    <AssemblyVersion>2.0.0.0</AssemblyVersion>
    <FileVersion>2.0.0.0</FileVersion>
</PropertyGroup>
```    
<br/>

And to make the methods in assembly A visible to another assembly B, you can use the following 2 ways.

<br/>

#### Set InternalsVisibleTo on top of a namespace in the project

```csharp
using System.Runtime.CompilerServices;
[assembly: InternalsVisibleTo("Service.UnitTests")]
```

![](./../../../assets/img/posts/2021-05-26-InternalProtectedMethodsUnitTest/1_set_internal_visible_in_class.PNG)

<br/>

#### Set InternalsVisibleTo in the project file

```csharp
<ItemGroup>
    <AssemblyAttribute Include="System.Runtime.CompilerServices.InternalsVisibleTo">
        <_Parameter1>Service.UnitTests</_Parameter1>
    </AssemblyAttribute>
</ItemGroup>
```

![](./../../../assets/img/posts/2021-05-26-InternalProtectedMethodsUnitTest/2_set_internal_visible_in_project_file.PNG)


<br/>
<br/>
<br/>

Now, let's check unit tests on protected methods.

![](./../../../assets/img/posts/2021-05-26-InternalProtectedMethodsUnitTest/3_protected_methods.PNG)

Due to the accessibility level limit, we have to create a sub class in the test project to access the method.

![](./../../../assets/img/posts/2021-05-26-InternalProtectedMethodsUnitTest/4_protected_methods_sub_class.PNG)

And then, you can use the call the method of sub class to test the protected method.

![](./../../../assets/img/posts/2021-05-26-InternalProtectedMethodsUnitTest/5_protected_methods_test.PNG)


That's it!

Now you have all the elements to make unit tests on internal methods and protected methods in .net core.

You can check the source code [here](https://github.com/hellomrsun/BlogCodeSource/tree/master/src/2021-05-26-Internal-Protected-Methods-Unit-Test).