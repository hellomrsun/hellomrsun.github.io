---
layout: post
read_time: true
show_date: true
title:  C# Delegate - MultiCast, Named, Anonymous, Lambda, EventHandler
date:   2013-05-29 08:00:00 +0100
description: C# Delegate - MultiCast, Named, Anonymous, Lambda, EventHandler
img: posts/uncategorized/csharp.jpg
tags: [CSharp]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/csharp-delegate-multicast-named-anonymous-lambda-event-handler.html'
---

A delegate is a type safe function pointer. Using delegates you can pass methods as parameters.

To pass a method as a parameter, to a delegate, the signature of the method must match the signature of the delegate. 

This is why, delegates are called type safe function pointers.

The declaration of a delegate type is similar to a method signature.

A delegate can be instantiated by associating it either with a named or anonymous method.

C# 2.0 introduced anonymous methods and in C# 3.0 and later, lambda expressions supersede anonymous methods as the preferred way to write inline code.

A simplified implementation of the Observer pattern

A simplified implementation of callbacks

Anonymous (non-reusable) blocks of code

1) Named delegate, multicast delegate

multiple delegate objects can be assigned to one delegate instance to be multicast using the + operator. A composed delegate calls the two delegates it was composed from. Only delegates of the same type can be composed.

The - operator can be used to remove a component delegate from a composed delegate.

![](./../../../assets/img/posts/2013-05-29-delegate/01.png)


In this example, "a" and "b" are simple delegates, "c" and "d" are multicast delegates.

![](./../../../assets/img/posts/2013-05-29-delegate/02.png)

2) Anonymous delegate & lambda

![](./../../../assets/img/posts/2013-05-29-delegate/03.png)

3) Event Handler delegate

Here I will create a custom event handler with two parameters which are an object sender and an custom object event args. 

custom "MyEventArgs" class inherite from class "EventArgs", with a class constructor who initiate the value for property "Arg".

![](./../../../assets/img/posts/2013-05-29-delegate/04.png)

Then, create custom event with custom event handler. 

The custom handle method has same parameters as custom event handler.

Then, bind handle method and event handler to event.

Instantiate a custom event args.

Invoke the event with class object and custom event args.

![](./../../../assets/img/posts/2013-05-29-delegate/05.png)

Let's see the result:

![](./../../../assets/img/posts/2013-05-29-delegate/06.png)

Now, the custom event handler is created.


Finally, we are arrived at the end of this article. I hope you can find some useful information for you. Enjoy coding!
