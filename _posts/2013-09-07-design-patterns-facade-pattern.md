---
layout: post
title: Design patterns V - Facade Pattern
description: Design patterns V - Facade Pattern
excerpt_separator:  <!--more-->
tags: Design-Patterns
canonical_url: 'https://sunjiangong.com/design-patterns-facade-pattern/'
---

Facade Pattern provides a unique interface to a set of methods of different subsystems in an application. It's widely used in application development.

It's a structural design pattern.

<!--more-->

Now let's see the implementation in C#.

Firstly, create subsystems and their methods.

```csharp
        class SubSytemOne
        {
            public void MethodOne()
            {
                Console.WriteLine("SubSystemOne Method");
            }
        }
        class SubSytemTwo
        {
            public void MethodTwo()
            {
                Console.WriteLine("SubSystemTwo Method");
            }
        }
        class SubSytemThree
        {
            public void MethodThree()
            {
                Console.WriteLine("SubSystemThree Method");
            }
        }
        class SubSytemFour
        {
            public void MethodFour()
            {
                Console.WriteLine("SubSystemThree Method");
            }
        }
```

Create Facade class and its methods as an interface to subsystems' methods' aggregation.
        
```csharp        
        class Facade
        {
            private readonly SubSytemOne _one;
            private readonly SubSytemTwo _two;
            private readonly SubSytemThree _three;
            private readonly SubSytemFour _four;
            public Facade()
            {
                _one = new SubSytemOne();
                _two = new SubSytemTwo();
                _three = new SubSytemThree();
                _four = new SubSytemFour();
            }
            public void MethodA()
            {
                Console.WriteLine("MethodA():");
                _one.MethodOne();
                _three.MethodThree();
            }
            public void MethodB()
            {
                Console.WriteLine("MethodB():");
                _two.MethodTwo();
                _four.MethodFour();
            }
            public void MethodC()
            {
                Console.WriteLine("MethodC():");
                _one.MethodOne();
                _two.MethodTwo();
                _four.MethodFour();
            }
        }
```

The clients can call facade's methods to satisfy its requirements.

```csharp
                var facade = new Facade();
                facade.MethodA();
                facade.MethodB();
                facade.MethodC();
```

So this is the implementation of facade pattern. I hope you enjoy this article. 

Enjoy coding!

