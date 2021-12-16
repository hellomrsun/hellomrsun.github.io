---
layout: post
read_time: true
show_date: true
title:  Unit tests best practices 
date:   2014-08-12 08:00:00 +0100
description: Unit tests best practices in csharp c# .net dotnet
img: posts/uncategorized/unit-test.PNG
tags: [UnitTest]
author: SUN Jiangong
mathjax: yes
redirect_from:
  - /2014/08/12/some-advice-on-unit-tests.html
---


Many of us have created unit tests and integration tests, but some tests could be very huge. 

Here are some advice:

#### 1. Keep test clean.

Separate each test with 3 sections: Arrange, Action, Assert.

<!--more-->

#### 2. Keep test small. 

By extracting the common code, you can make a large part of your test reusable.

Here is an test skeleton:

```csharp
[TestFixture]
public class Tests
{
	[SetUp]
	public void Init()
	{
	}
 
	[Test]
	public void SpecificTest_One()
	{
		//ARRANGE
		//ACTION
		//ASSERT
	}
 
	[Test]
	[Explicit]
	public void SpecificTest_Two()
	{
		//ARRANGE
		//ACTION
		//ASSERT
	}
	
	[TearDown]
	public void TearDown()
	{          
	}
}
```


Enjoy coding!

