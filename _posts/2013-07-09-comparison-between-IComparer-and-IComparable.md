---
layout: post
read_time: true
show_date: true
title:  Comparison between IComparer and IComparable in CSharp
date:   2013-07-09 08:00:00 +0100
description: Comparison between IComparer and IComparable in CSharp
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/comparison-between-IComparer-and-IComparable-in-CSharp.html'
---


I've already written an article introducing the usage of comparer here. In this article I'll compare the usage of IComparable and IComparer with examples.


**Important difference**:  A class can have only one Comparable, but multiple Comparers.

<!--more-->

Here I have a class Student with different properties, which will be used as sorting criterias.

```csharp
public class Student : IComparable<Student>
{
    public string LastName { get; set; }
    public string FirstName { get; set; }
    public int Age { get; set; }
    public int Class { get; set; }
}
```

Firstly, I want class Student to implement interface IComparable, and I must override method CompareTo of interface IComparable. In this method I sort Student list in an ascending order.

```csharp
//class who implement interface IComparable, must implement CompareTo method
public class Student : IComparable<Student>
{
    public string LastName { get; set; }
    public string FirstName { get; set; }
    public int Age { get; set; }
    public int Class { get; set; }
    //CompareTo method compare itself to another object
    public int CompareTo(Student student)
    {
        return LastName.CompareTo(student.LastName);
    }
}
```

In this way, Student list will be sorted by LastName in an ascending order.

Next, I'll create 3 comparers who will use the rest 3 properties as sorting criteria.

```csharp
//Comparer 1
//class who implement interfce IComparer, must implement Compare method
public class OrderByAgeAscending : IComparer<Student>
{
    //Compare method compares two objects
    public int Compare(Student x, Student y)
    {
        if (x.Age.CompareTo(y.Age) < 0)
        {
            return -1;
        }
        if (x.Age.CompareTo(y.Age) == 0)
        {
            return 0;
        }
        return 1;
    }
}

//Comparer 2
public class OrderByClassDescending : IComparer<Student>
{
    public int Compare(Student x, Student y)
    {
        if (x.Class.CompareTo(y.Class) < 0)
        {
            return 1;
        }
        if (x.Class.CompareTo(y.Class) == 0)
        {
            return 0;
        }
        return -1;
    }
}

//Comparer 3
public class OrderByFirstNameAscending : IComparer<Student>
{
    public int Compare(Student x, Student y)
    {
        if (x.FirstName.CompareTo(y.FirstName) < 0)
        {
            return -1;
        } if (x.FirstName.CompareTo(y.FirstName) == 0)
        {
            return 0;
        }
        return 1;
    }
}
```

Now I will create a new Student list with some Students and try to sort them with comparable and comparer.
Firstly, I will create a list.

```csharp
var s1 = new Student() { LastName = "charles", FirstName = "charles", Age = 27, Class = 15 };
var s2 = new Student() { LastName = "viz", FirstName = "newton", Age = 20, Class = 30 };
var s3 = new Student() { LastName = "la", FirstName = "aba", Age = 2, Class = 2 };
var students = new List<Student>() { s1, s2, s3 };
```

Then, I will sort the list with comparable. I just need to call Sort() method, it will use the CompareTo() method I've created.

```csharp
//IComparable: sort by last name
students.Sort();
Display(students, "IComparable OrderByLastName:");
```

And then, I will use the 3 comparers to sort the list.

```csharp
//Comparer 1: order by age
var c1 = new OrderByAgeAscending();
students.Sort(c1);
Display(students, "Comparer OrderByAgeAscending:");

//Comparer 2: order by class
var c2 = new OrderByClassDescending();
students.Sort(c2);
Display(students, "Comparer OrderByClassDescending:");

//Comparer 3: order by first name 
var c3 = new OrderByFirstNameAscending();
students.Sort(c3);
Display(students, "Comparer OrderByFirstNameAscending");
```

And there are an Display() method who is in charge of display the student information.

```csharp
public static void Display(List<Student> students, string comparerName)
{
    Console.WriteLine(comparerName);
    foreach (var student in students)
    {
        Console.WriteLine("last name: " + student.LastName + "; first name: " + student.FirstName + "; age: " + student.Age + "; class: " + student.Class);
    }
}
```

Now, let's see the results:

![](./../../../assets/img/posts/2013-07-09-icomparer-icomparable/01.png)

Right now, we are arrived at the end of the article. I hope you can find useful information here. Enjoy coding!
