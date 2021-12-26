---
layout: post
read_time: true
show_date: true
title:  Design pattern IV - Decorator/Wrapper pattern
date:   2013-06-08 08:00:00 +0100
description: Design pattern IV - Decorator/Wrapper pattern
img: posts/uncategorized/design-patterns.PNG
tags: [DesignPatterns]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/design-pattern-IV-decorator-wrapper-pattern.html'
---

Decorators provide a flexible alternative to subclassing for extending functionality.

<!--more-->

```csharp
public class DecoratorPattern
{
        /*
        * decorator和wrapper是一个设计模式
        * 用途：用来扩展已有类的功能
        * 实现步骤：
        * 先定义一个interface，然后建立一个类继承这个接口，并实现接口里的方法
        * 建立一个包装类继承同一个接口，并在这个包装类的构造器中使用接口的实例做参数。
        * 建立实际包装类继承包装类，重写接口定义的方法，并可以创建自己特有的方法。
        */
    public interface IComponent
    {
        void Operation();
    }

    public class ConcreteComponent : IComponent
    {
        public void Operation()
        {
            Console.WriteLine("ConcreteComponent operation");
        }
    }

    public class Decorator : IComponent
    {
        private readonly IComponent _decoratedComponent;

        public Decorator(IComponent iComponent)
        {
            _decoratedComponent = iComponent;
        }

        public void Operation()
        {
            _decoratedComponent.Operation();
        }
    }

    public class ConcreteDecoratorA : Decorator
    {
        private string _addState;

        public ConcreteDecoratorA(Decorator decorator)
            : base(decorator)
        {
        }

        public new void Operation()
        {
            base.Operation();
            _addState = "New State";
            Console.WriteLine("ConcreteDecoratorA.Operation");
        }
        public void CustomOperation()
        {
            Console.WriteLine("ConcreteDecoratorA custom Operation");
        }
    }

    public static void Main()
    {
        ConcreteComponent concreteComponent = new ConcreteComponent();
        concreteComponent.Operation();

        Decorator decorator = new Decorator(concreteComponent);
        ConcreteDecoratorA concreteDecoratorA = new ConcreteDecoratorA(decorator);
        concreteDecoratorA.Operation();
        concreteDecoratorA.CustomOperation();

        Console.ReadKey();
    }
}
```

