---
layout: post
read_time: true
show_date: true
title:  Software Craftsmanship - How to implement Open Closed Principle
date:   2013-07-05 07:00:00 +0100
description: Software Craftsmanship - How to implement Open Closed Principle
img: posts/uncategorized/craftsman.PNG
tags: [Craftsmanship]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/software-craftsmanship-how-to-implement-open-closed-principle.html'
---


S.O.L.I.D (Single responsibility, Open-closed, Liskov substitution, Interface segregation and Dependency inversion) are object oriented design principles, which are best practices for OOP software development.


Open Closed Principle means: open for extension, closed for modification.

For example: when there are some new functionalities coming, minimize the modification of exsiting code, and just add new class, new code to extend it.

<!--more-->

Here I've made an example for demonstrating open closed principle.


There are three cars with their properties

```csharp
public class Peugeot107
{
    public string Name { get; set; }
    public int PriceFactor1 { get; set; }
    public int PriceFactor2 { get; set; }
}

public class Peugeot208
{
    public string Name { get; set; }
    public int PriceFactor1 { get; set; }
    public int PriceFactor2 { get; set; }
}

public class Peugeot307
{
    public string Name { get; set; }
    public int PriceFactor1 { get; set; }
    public int PriceFactor2 { get; set; }
}
```

Here we calculate their prices

```csharp
public class Car
{
    public double PriceCalculate(object car)
    {
        double price = new double();
        if (car is Peugeot107)
        {
            Peugeot107 x = (Peugeot107)car;
            price = 10 * x.PriceFactor1 + x.PriceFactor2;
        }
        else if (car is Peugeot208)
        {
            Peugeot208 x = (Peugeot208)car;
            price = 10 * x.PriceFactor1 * x.PriceFactor2;
        }
        else if (car is Peugeot307)
        {
            Peugeot307 x = (Peugeot307)car;
            price = 10 * x.PriceFactor1 + 30 * x.PriceFactor2;
        }
        return price;
    }
}
```

In this case, when we need to add new cars, we need to modify the method "PriceCalculate" which doesn't respect open closed principle.

Now, we will see how to optimize it with open closed principle.

Firstly, we create an interface and declare a method in it.

```csharp
public interface ICar
{
    double PriceCalculator();
}
```

Then, create several car classes who implement this interface.

```csharp
public class Peugeot107 : ICar
{
    public string Name { get; set; }
    public int PriceFactor1 { get; set; }
    public int PriceFactor2 { get; set; }
    public double PriceCalculator()
    {
        return 10 * PriceFactor1 + PriceFactor2;
    }
}
public class Peugeot208 : ICar
{
    public string Name { get; set; }
    public int PriceFactor1 { get; set; }
    public int PriceFactor2 { get; set; }
    public double PriceCalculator()
    {
        return 10 * PriceFactor1 * PriceFactor2;
    }
}
public class Peugeot307 : ICar
{
    public string Name { get; set; }
    public int PriceFactor1 { get; set; }
    public int PriceFactor2 { get; set; }
    public double PriceCalculator()
    {
        return 10 * PriceFactor1 + 30 * PriceFactor2;
    }
}
```


In this way, if we want to add new cars, we just need to add a new car class and implement its own price calculation. The application is extended, and not modified.

I hope you enjoy this article. Enjoy coding!