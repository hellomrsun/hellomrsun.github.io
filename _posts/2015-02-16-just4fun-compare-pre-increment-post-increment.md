---
layout: post
title: Just4Fun - play with PreIncrement and PostIncrement in csharp
description: Just4Fun - play with PreIncrement and PostIncrement in csharp
excerpt_separator:  <!--more-->
tags: Just4Fun
canonical_url: 'https://sunjiangong.com/just-for-fun-play-with-pre-increment-and-post-increment-in-csharp/'
---

Pre-Increment and Post-Increment are used frequently in conditions for loops.

Here we are playing a calculation game with Post-Increment and Pre-Increment.

<!--more-->

Example 1:

```csharp
int i = 10;
Console.WriteLine(i++); //=> 10
Console.WriteLine(i); //=> 11
```

Example 2:

```csharp
int i = 10;
Console.WriteLine(++i); //=> 11
Console.WriteLine(i); //=> 11
```

Example 3:

```csharp
int i = 10;
Console.WriteLine(i--); //=> 10
Console.WriteLine(i); //=> 9
```

Example 4:

```csharp
int i = 10;
Console.WriteLine(--i); //=> 9
Console.WriteLine(i); //=> 9
```

Example 5:

```csharp
int i = 5;
var result1 = i++ + ++i;
Console.WriteLine(string.Format("i=5; i++ + ++i result is : '{0}'", result1)); //=> 12

i = 5;
var result2 = ++i + i++;
Console.WriteLine(string.Format("i=5; ++i + i++ result is : '{0}'", result2)); //=> 12

i = 5;
var result3 = i++ - ++i;
Console.WriteLine(string.Format("i=5; i++ - ++i result is : '{0}'", result3)); //=> -2

i = 5;
var result4 = ++i - ++i;
Console.WriteLine(string.Format("i=5; ++i - ++i result is : '{0}'", result4)); //=> -1

i = 5;
var result5 = ++i - i++;
Console.WriteLine(string.Format("i=5; ++i - i++ result is : '{0}'", result5)); //=> 0

i = 5;
var result6 = i++ + i++;
Console.WriteLine(string.Format("i=5; i++ + i++ result is : '{0}'", result6)); //=> 11
```

Example 6:

```csharp
int i = 5;
var result1 = i-- + --i;
Console.WriteLine(string.Format("i=5; i-- + --i result is : '{0}'", result1)); //=> 8

i = 5;
var result2 = --i + i--;
Console.WriteLine(string.Format("i=5; --i + i-- result is : '{0}'", result2)); //=> 8

i = 5;
var result3 = i-- - --i;
Console.WriteLine(string.Format("i=5; i-- - --i result is : '{0}'", result3)); //=> 2

i = 5;
var result4 = --i - --i;
Console.WriteLine(string.Format("i=5; --i - --i result is : '{0}'", result4)); //=> 1

i = 5;
var result5 = --i - i--;
Console.WriteLine(string.Format("i=5; --i - i-- result is : '{0}'", result5)); //=> 0

i = 5;
var result6 = i-- + i--;
Console.WriteLine(string.Format("i=5; i-- + i-- result is : '{0}'", result6)); //=> 9
```