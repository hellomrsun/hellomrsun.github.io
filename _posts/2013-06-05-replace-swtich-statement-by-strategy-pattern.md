---
layout: post
read_time: true
show_date: true
title:  Refactoring - replace Switch statement with state/strategy
date:   2013-06-05 08:00:00 +0100
description: Refactoring - replace Switch statement with state/strategy
img: posts/uncategorized/design-patterns.PNG
tags: [Craftsmanship, DesignPatterns]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/replace-swtich-statement-by-strategy-pattern.html'
---


Switch statements is procedural structure, not object programming, it can be replaced by strategy pattern with implementation of interface/abstract strategy, with concrete strategies.

<!--more-->

```csharp
public class SwitchToReplace
{
    public static void Main()
    {
        Console.WriteLine(Get(Instruments.Telephone));
        Console.WriteLine(Get(Instruments.Mobile));
        Console.WriteLine(Get(Instruments.Television));
        Console.WriteLine(Get(Instruments.Guitar));
        Console.ReadLine();
    }

    public enum Instruments
    {
        Telephone,
        Mobile,
        Television,
        Guitar
    }

    public static string Get(Instruments instruments)
    {
        string value;
        switch (instruments)
        {
            case Instruments.Telephone:
                Console.WriteLine("Case 1");
                value = "Telephone";
                break;
            case Instruments.Mobile:
                Console.WriteLine("Case 2");
                value = "Mobile";
                break;
            case Instruments.Television:
                Console.WriteLine("Case 3");
                value = "Television";
                break;
            default:
                Console.WriteLine("Default case");
                value = "Default case";
                break;
        }
        return value;
    }
}
```

Replace Switch statement with State/Strategy pattern

```csharp
public class SwitchReplaced
{
    public enum InstrumentEnum
    {
        Telephone,
        Mobile,
        Television,
        Guitar
    }
    //define an abstract class and its method signature
    public abstract class Instrument
    {
        public abstract string GetInstrumentName();
    }
    //inherit abstract class and override it's method
    public class InstrumentTelephone : Instrument
    {
        public override string GetInstrumentName()
        {
            Console.WriteLine("Case 1");
            return "Telephone";
        }
    }
    public class InstrumentMobile : Instrument
    {
        public override string GetInstrumentName()
        {
            Console.WriteLine("Case 2");
            return "Mobile";
        }
    }
    public class InstrumentTelevision : Instrument
    {
        public override string GetInstrumentName()
        {
            Console.WriteLine("Case 3");
            return "Television";
        }
    }
    public class InstrumentGuitar : Instrument
    {
        public override string GetInstrumentName()
        {
            Console.WriteLine("Case 4");
            return "Guitar";
        }
    }
    public class InstrumentContext
    {
        private readonly Instrument _instrumentInstance;
        //put abstract class Instrument's instance in constructor, assign it to local variable
        public InstrumentContext(Instrument instrument)
        {
            _instrumentInstance = instrument;
        }
        //Invoke method of concrete strategy
        public string InvokeGetInstrumentName()
        {
            return _instrumentInstance.GetInstrumentName();
        }
    }
    //Extract same calling code in a single method
    public string InstrumentInfo(Instrument instrument)
    {
        InstrumentContext context = new InstrumentContext(instrument);
        return context.InvokeGetInstrumentName();
    }

    public static void Main()
    {
        SwitchReplaced sr = new SwitchReplaced();
        //call
        Console.WriteLine(sr.InstrumentInfo(new InstrumentGuitar()));
        Console.WriteLine(sr.InstrumentInfo(new InstrumentMobile()));
        Console.ReadLine();
    }
}
```

I hope this post can do help to you! enjoy coding!
