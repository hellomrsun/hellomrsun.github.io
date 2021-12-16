---
layout: post
read_time: true
show_date: true
title:  Just4Fun - compare const and readonly in C#
date:   2015-03-13 08:00:00 +0100
description: Just4Fun - compare const and readonly in C#, CSharp
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
mathjax: yes
redirect_from:
  - /2015/03/13/just4fun-compare-const-and-readonly.html
---

Today let us talk about const and readonly.

const is considered as compile-time constant.

readonly is considered as runtime constant.

I will demonstrate some example code to clarify their usages and differences.

<!--more-->

### I. Const usages

<br/>

Firstly, you can see that const variable can be declared and assigned at class level.

```csharp
public class ConstExample
{
    public const string CstValue1 = "hello"; //Correct
}
```

You can also declare a const variable in constructor

```csharp
public ConstExample()
{
    const string cstValue6 = "hehe"; //Correct
}
```

You can see that const can be declared at method level too

```csharp
public void Display()
{
    const string cstValue2 = "cst 2"; //Correct : Constant can be declared in method
}
```

If you want to assign another value to CstValue1, you will get an compile-time exception. Because const can only be assigned when declaration.

```csharp
CstValue1 = "hello2"; //Compile time exception : Can not resolve symbol CstValue1
```

You can not also assign another value to CstValue1 in the constructor. You will get an compile-time exception.

```csharp
public ConstExample()
{
    CstValue1 = "hello2"; //Compile time exception : Constant can not be used as an assignment target
}
```

May be you want to assign a normal string variable to a const like this. But you will see it doesn’t work too.

```csharp
public string v1;
const string CstValue2 = v1; //Compile time exception : Constant initializer must be compile-time constant
```

But you can assign the operation result of several consts to another const like this.

```csharp
public const string CstValue3 = "world"; //Correct

public const string CstValue4 = CstValue1 + CstValue3; //Correct : Constants can only be assigned with values or with consts
```


You can also declare a const, and assign it with the addition of two consts in the method.

```csharp
const string cstValue5 = CstValue1 + CstValue3;
```

When you display them you can see

```csharp
Console.WriteLine(CstValue1); //=> hello

Console.WriteLine(cstValue2); //=> cst 2

Console.WriteLine(CstValue4); //=> helloworld

Console.WriteLine(cstValue5); //=> helloworld
```

<br/>

### II. readonly usages

<br/>

Firstly, you can declare an readonly variable at class level.

```csharp
public class ReadOnlyExample
{
    public readonly string rdValue1 = "good";
}
```

You can also just declare a readonly variable without assigning any value to it.

```csharp
public readonly string rdValue2;
```

You can not declare a readonly variable in a method.

```csharp
readonly string rdValue6 = "hohoho"; //compile time exception : statement expected
```

You cannot assign a value to variable rdValue1 after the declaration, except for, you assign a value in the class constructor.

```csharp
rdValue1 = "good 2"; //Compile time exception : Can not resolve symbol rdValue1
```

You can not assign a readonly variable to another readonly variable at class level.

```csharp
readonly string rdValue3 = rdValue1; //Compile time exception : cannot access non-static field 'rdValue1' in static context
```

You can not assign a normal variable to a readonly variable neither at class level.

```csharp
public string value1 = "hey";
readonly string rdValue6 = value1; //Compile time exception : cannot access non-static field 'value1' in static context
```

You can not assign value to a readonly variable in a method.

```csharp
public void Display()
{
    rdValue1 = "good one"; //Compile time exception: Readonly field can not be used as an assignment target
    rdValue2 = "good too"; //Compile time exception: Readonly field can not be used as an assignment target
}
```


But you can assign a normal variable to a readonly variable in class constructor.
You can even assign the operation result of several readonly variables to another readonly variable.

```csharp
public readonly string rdValue4;

public readonly string rdValue5;

public ReadOnlyExample(string value)
{
    rdValue2 = value; //Correct

    rdValue4 = rdValue1 + rdValue2; //Correct : Assign another readonly variable to another readonly variable can only be done in constructor

    rdValue5 = rdValue1 + value1; //Correct : Assign readonly variable with normal variable to another readonly variable
}
```


when you display them, you will see

```csharp
Console.WriteLine(rdValue1); //=> good

Console.WriteLine(rdValue2); //=> day

Console.WriteLine(rdValue4); //=> goodday

Console.WriteLine(rdValue5); //=> goodhey
```

If you want to access to a const, you must access it via the class

```csharp
Console.WriteLine(ConstExample.CstValue1); //Const variable can only be accessed by class
```

If you want to access to a readonly variable, you must access it via an instance of class.

```csharp
var re = new ReadOnlyExample("day");
Console.WriteLine(re.rdValue1); //Readonly value can only be accessed by instance of class
```

<br/>

So to conclude,

**Const :**

- Can only be assigned at declaration
- Can be declared at class level, in constructor and in method.
- Can be assigned with operation result of several consts at class level or in constructor or in method. (like addition, multiplication
etc)
- Once the declaration is done, you can never modify a const’s value, neither in constructor, nor just after declaration.
- You can access const variable only by class.

**Readonly:**

- Can only be assigned at declaration or in constructor.
- Can be declared only at class level. You can declare a readonly variable neither in constructor nor in method.
- Can be assigned with operation result of several readonly variables only in constructor (like addition, multiplication etc). You can not assign them to a readonly variable when declaration or in a method.
- You can access Readonlyvariable only by the instance of class.


I hope you find this article helpful!

