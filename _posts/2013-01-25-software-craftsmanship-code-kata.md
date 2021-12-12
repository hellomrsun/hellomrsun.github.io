---
layout: post
read_time: true
show_date: true
title:  Software craftsmanship - code Kata
date:   2013-01-25 08:00:00 +0100
description: Software craftsmanship, code kata, best practice, .NET, Dotnet, C#, Csharp, Agile, Paris Software Craftsmanship
img: posts/uncategorized/craftsman.PNG 
tags: [Craftsmanship]
author: SUN Jiangong
mathjax: yes
---

I have participated in a session organized by **Paris Software Craftsmanship Community** yesterday on 24 January 2013; I was among 20 passionate developers who like to optimize and accelerate their project development and sharpen their expertise. 

Thanks for the organizers **Jean Laurent de Morlhon** and **Cyrille Martraire** and the other active members of this group. I have practiced "code kata" method, refactored and tested a program. 

<br />

##### What is kata?

*Kata is a Japanese word (型 or 形) meaning “form”. It refers to a detailed choreographed pattern of martial arts movements made to be practiced alone. It can also be reviewed within groups and in unison when training. It is practiced in Japanese martial arts as a way to memorize and perfect the movements being executed.*

![](./../../../assets/img/posts/2013-01-25-code-kata/code-kata.jpg)

<br />

##### Code Kata

Code Kata is an attempt to bring this kind of practice into software development. The intent behind code kata is similar. 

You can pick a programming subject and try to implement it. Then try to implement it again from scratch with some little improvements. Then repeat and repeat again.

<br />

##### The subject: "Gilded Rose"

Here is an original code GildedRose.

It is a little messy. We need to write and improve it in each repetition.

```csharp
using System.Collections.Generic;

namespace csharp
{
    public class GildedRose
    {
        IList<Item> Items;
        public GildedRose(IList<Item> Items)
        {
            this.Items = Items;
        }

        public void UpdateQuality()
        {
            for (var i = 0; i < Items.Count; i++)
            {
                if (Items[i].Name != "Aged Brie" && Items[i].Name != "Backstage passes to a TAFKAL80ETC concert")
                {
                    if (Items[i].Quality > 0)
                    {
                        if (Items[i].Name != "Sulfuras, Hand of Ragnaros")
                        {
                            Items[i].Quality = Items[i].Quality - 1;
                        }
                    }
                }
                else
                {
                    if (Items[i].Quality < 50)
                    {
                        Items[i].Quality = Items[i].Quality + 1;

                        if (Items[i].Name == "Backstage passes to a TAFKAL80ETC concert")
                        {
                            if (Items[i].SellIn < 11)
                            {
                                if (Items[i].Quality < 50)
                                {
                                    Items[i].Quality = Items[i].Quality + 1;
                                }
                            }

                            if (Items[i].SellIn < 6)
                            {
                                if (Items[i].Quality < 50)
                                {
                                    Items[i].Quality = Items[i].Quality + 1;
                                }
                            }
                        }
                    }
                }

                if (Items[i].Name != "Sulfuras, Hand of Ragnaros")
                {
                    Items[i].SellIn = Items[i].SellIn - 1;
                }

                if (Items[i].SellIn < 0)
                {
                    if (Items[i].Name != "Aged Brie")
                    {
                        if (Items[i].Name != "Backstage passes to a TAFKAL80ETC concert")
                        {
                            if (Items[i].Quality > 0)
                            {
                                if (Items[i].Name != "Sulfuras, Hand of Ragnaros")
                                {
                                    Items[i].Quality = Items[i].Quality - 1;
                                }
                            }
                        }
                        else
                        {
                            Items[i].Quality = Items[i].Quality - Items[i].Quality;
                        }
                    }
                    else
                    {
                        if (Items[i].Quality < 50)
                        {
                            Items[i].Quality = Items[i].Quality + 1;
                        }
                    }
                }
            }
        }
    }
}
```

<br />

We add unit tests to ensure the behaviors of code are always correct. Then, we refactor the code with method extraction, if-else inversion to make it cleaner, easier to understand and maintain. Because visibility, maintainability, scalability are very important aspects in programming which could be ignored in daily work.

The code become a lot cleaner after several katas.

You can try to practice code kata yourself too. And there are a lot of interesting subjects.

Here is a non-exhaustif list of code katas you can practice:

- Algorithmic
  - KataBankOCR
  - KataFizzBuzz
  - FooBarQix
  - KataPotter
  - KataRomanNumerals
  - KataRomanCalculator
  - KataNumbersInWords
  - KataArgs
  - KataAnagram
  - KataDepthFirstSearch
  - KataNumberToLCD

- Game Modeling:
  - KataBowling
  - KataGameOfLife
  - KataMastermid
  - KataMinesweeper
  - KataPacMan
  - KataPokerHands
  - KataReversi
  - KataTennis
  - KataTexasHoldEm
  - KataTradingCardGame
  - KataYahtzee

- Math Oriented
  - KataRange
  
- String manipulation
  - KataDictionaryReplacer
  - KataWordWrap

- Specific Technologies
  - KataQotdCgi
  - KataJEEWebAuthentication

- Refactoring legacy code & Design Principles
  - TDDMicroExercises

- Design Principles
  - TensionsAndSynergiesBetweenDesignPrinciples
  - ObjectsRelationshipsCodingDojo

You can find the details on [CodingDoJo](https://codingdojo.org/KataCatalogue/){:target="_blank"}.

There are alos some good materials to read on [CodeKata](http://codekata.com/){:target="_blank"}.