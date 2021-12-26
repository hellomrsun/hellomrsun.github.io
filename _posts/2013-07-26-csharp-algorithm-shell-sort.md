---
layout: post
read_time: true
show_date: true
title:  Shell sort 
date:   2013-07-26 08:00:00 +0100
description: Shell sort in csharp
img: posts/uncategorized/algorithm.PNG
tags: [Algorithm]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/shell-sort-in-csharp.html'
---


Shell algorithm is a sorting algorithm. 

The principle is use a interval for switching two values' positions, and the interval will also reduce, like from 9 to 8 to 7 to 5 ...0

<!--more-->

Here is an implementation in CSharp.


```csharp
public static void ShellSort(int[] numbers, int size)
{
    int i, j, increment, temp;
    increment = 3;
    while (increment > 0)
    {
        for (i = 0; i < size; i++)
        {
            j = i;
            temp = numbers[i];
            while ((j >= increment) && (numbers[j - increment] > temp))
            {
                numbers[j] = numbers[j - increment];
                j = j - increment;
            }
            numbers[j] = temp;
        }

        if (increment / 2 != 0)
        {
            increment = increment / 2;
        }
        else if (increment == 1)
        {
            increment = 0;
        }
    }
}
```

To test it, you just need to initialize an array or list.

```csharp
public static void Main()
{
    int[] arr = { 20, 5, 6, 100, 899, 4, 20, 9, 18, 29, 0 };
    Console.WriteLine("Before shell sort:");
    Display(arr);

    ShellSort(arr, arr.Length);

    Console.WriteLine("After shell sort:");
    Display(arr);

    Console.ReadKey();
}
```

I hope you will like this post! Enjoy coding!