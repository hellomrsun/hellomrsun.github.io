---
layout: post
read_time: true
show_date: true
title:  Design Patterns VI Simple Factory, Factory Method, Abstract Factory
date:   2014-01-04 08:00:00 +0100
description: Introduction to Design Patterns Simple Factory, Factory Method, Abstract Factory
img: posts/uncategorized/design-patterns.PNG
tags: [DesignPatterns]
author: SUN Jiangong
mathjax: yes
redirect_from:
  - /2014/01/04/design-patterns-simple-factory-factory-method-abstract-factory.html
---


I want to introduce the factory patterns here, including Simple Factory, Factory Method and Abstract Factory.

As the name simple factory implies, you have a factory class to create different objects depending on your requirement. All your logic will be included in the factory class.

So if you have new types of objects to create in your code, you have to modify your factory class to extend it.

<!--more-->

Here is an example :


You have an interface IProduct, and some real product types implement it.

```csharp
public interface IProduct
{
    int GetPrice();
}

public class Toy : IProduct
{
    public int GetPrice()
    {
        return 100;
    }
}

public class Cloth : IProduct
{
    public int GetPrice()
    {
        return 200;
    }
}
```

There is an enum for product types

```csharp
public enum ProductType
{
    Toy,
    Cloth
}
```

In your factory class,

```csharp
public class ProductFactory
{
    public IProduct CreateProduct(ProductType productType)
    {
        IProduct product;
        switch (productType)
        {
            case ProductType.Toy:
                product = new Toy();
                break;
            case ProductType.Cloth:
                product = new Cloth();
                break;
            default:
                throw new InvalidDataException();
        }

        return product;
    }
}
```

When you test your factory class, you can use the following example:

```csharp
public static void Main()
{
    var productFactory = new ProductFactory();
    var toy = productFactory.CreateProduct(ProductType.Toy);
    var cloth = productFactory.CreateProduct(ProductType.Cloth);
    Console.WriteLine(toy.GetPrice());
    Console.WriteLine(cloth.GetPrice());
}
```

And if you want to add new product types, you need to modify the switch clause to adapt your changes, which is not recommended.


Next, we will discover **factory method pattern**. 

It will be more abstract, and supports better the extensiveness of applications. 

We have the same IProduct interface, Toy and Cloth class as the previous example. But this time we will have an abstract factory and some real factories who inherit it.

Here is the example:

We use an abstract class to create a type of product.

```csharp
public abstract class ProductFactory
{
    public abstract IProduct CreateProduct();
}
```

The real factory to create relevant product.

```csharp
public class ToyFactory : ProductFactory
{
    public override IProduct CreateProduct()
    {
        return new Toy();
    }
}

public class ClothFactory : ProductFactory
{
    public override IProduct CreateProduct()
    {
        return new Cloth();
    }
}
```

When we test the the classes, we will use the specific factory to create a specific product. In case of new types of factory, just create them and inherit the abstract factory.

```csharp
public static void Main()
{
    var toyFactory = new ToyFactory();
    var toy = toyFactory.CreateProduct();
    var clothFactory = new ClothFactory();
    var cloth = clothFactory.CreateProduct();
    Console.WriteLine(toy.GetPrice());
    Console.WriteLine(cloth.GetPrice());
}
```


Next, we will discover **abstract factory pattern**. 

Abstract factory pattern is a combination of several different types of objects. It's kind of advanced version of factory method.


Here is the example:

We have the IProduct interface and its child interfaces as IToy and ICloth. An enum for cloth type.

```csharp
public enum ClothType
{
    Man,
    Woman,
    Boy,
    Girl
}

public interface IProduct
{
    int GetPrice();
}

public interface IToy : IProduct
{
    new int GetPrice();
    string GetToyName();
}

public interface ICloth : IProduct
{
    new int GetPrice();
    ClothType GetClothType();
}
```

Nike and Adidas has their own way to produce their toys and clothes. So we have the following classes.

```csharp
public class NikeToy : IToy
{
    private readonly string _toyName;

    public NikeToy(string toyName)
    {
        _toyName = toyName;
    }

    public int GetPrice()
    {
        return 100;
    }
    public string GetToyName()
    {
        return _toyName;
    }
}

public class AdidasToy : IToy
{
    private readonly string _toyName;

    public AdidasToy(string toyName)
    {
        _toyName = toyName;
    }

    public int GetPrice()
    {
        return 200;
    }
    public string GetToyName()
    {
        return _toyName;
    }
}

public class NikeCloth : ICloth
{
    private ClothType _clothType;
    public NikeCloth(ClothType clothType)
    {
        _clothType = clothType;
    }
    public int GetPrice()
    {
        return 300;
    }
    public ClothType GetClothType()
    {
        return _clothType;
    }
}

public class AdidasCloth : ICloth
{
    private ClothType _clothType;
    public AdidasCloth(ClothType clothType)
    {
        _clothType = clothType;
    }
    public int GetPrice()
    {
        return 400;
    }
    public ClothType GetClothType()
    {
        return _clothType;
    }
}
```

Then we create an abstract factory which can produce toys and clothes.

```csharp
public abstract class AbstractFactory
{
    public abstract IToy GetToy();
    public abstract ICloth GetCloth(ClothType clothType);
}
```

Then Nike and Adidas have their own factories to produces toys and clothes.

```csharp
public class NikeFactory : AbstractFactory
{
    public override IToy GetToy()
    {
        return new NikeToy("hello kity");
    }

    public override ICloth GetCloth(ClothType clothType)
    {
        return new NikeCloth(clothType);
    }
}

public class AdidasFactory : AbstractFactory
{
    public override IToy GetToy()
    {
        return new AdidasToy("tiger");
    }

    public override ICloth GetCloth(ClothType clothType)
    {
        return new AdidasCloth(clothType);
    }
}
```

Let's test it.

```csharp
public static void Main()
{
    var nike = new NikeFactory();
    Console.WriteLine(nike.GetToy().GetPrice());
    Console.WriteLine(nike.GetToy().GetToyName());
    Console.WriteLine(nike.GetCloth(ClothType.Girl).GetClothType());
    Console.WriteLine(nike.GetCloth(ClothType.Girl).GetPrice());

    var adidas = new AdidasFactory();
    Console.WriteLine(adidas.GetToy().GetPrice());
    Console.WriteLine(adidas.GetToy().GetToyName());
    Console.WriteLine(adidas.GetCloth(ClothType.Boy).GetClothType());
    Console.WriteLine(adidas.GetCloth(ClothType.Boy).GetPrice());
}
```

As you have seen, we have more granularity about the production of toys and clothes. And even more, we could have more fine-grained design for this small system.

So, here is my explanation of the different factory patterns. 

If you have different opinions or insights, you could leave your comments. :)

Enjoy coding!!!
