---
layout: post
title: Unit tests practices
description: Unit tests practices
excerpt_separator:  <!--more-->
tags: Unit-Test
canonical_url: 'https://sunjiangong.com/unit-tests-practices/'
---


Many of us have created unit tests and integration tests, but some tests could be very huge. 

Here are some advice:

#### 1. Keep test clean.

Separate each test with 3 sections: Arrange, Action, Assert.

#### 2. Keep test small. 

By extracting the common code, you can make a large part of your test reusable.

<!--more-->

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

