---
layout: post
read_time: true
show_date: true
title:  Microsoft Techdays 2015 - Etat de lieux JavaScript
date:   2015-02-16 08:00:00 +0100
description: Microsoft Techdays 2015 - Etat de lieux JavaScript
img: posts/2015-02-16-TechdaysEtatDeLieuxJavascript/01.png
tags: [Craftsmanship]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/microsoft-techdays-2015-etat-de-lieux-javascript.html'
---


This is a great introduction session about mostly used JavaScript libraries in the market.

Each library is presented in three parts:
- History
- Usage
- Demo

Firstly, it’s the leading library jQuery which makes javascript modern and easy-to-use. This library has changed a lot of people’s view about JavaScript.

<!--more-->

It was created by John Resig on Janurary 2006. It has improved developer’s productivity a lot and it supports multiple browsers.

You can access the DOM elements with $ and specify the behavior to selected element(s).

Here are some examples:

```javascript
$("div#idName").text("helloworld");
$("div.className").text("helloworld");
$("a").click(function(){ alert("hello world");});
```


![](./../../../assets/img/posts/2015-02-16-TechdaysEtatDeLieuxJavascript/01.png)

When you need to install different javascript or css libraries, you could use Bower to download and install them. Bower is a package manager for client side packages. Just like Nuget for server side packages in visual studio.

BootStrap is a javascript and css library created by Twitter on 2011. It’s a mobile-first library because twitter is oriented to mobile phones. It can adapt your websites to all kinds of different screens like PC screen and mobile screen.

![](./../../../assets/img/posts/2015-02-16-TechdaysEtatDeLieuxJavascript/02.png)

A screen is divided by 12 columns and you can design the web pages using columns.

![](./../../../assets/img/posts/2015-02-16-TechdaysEtatDeLieuxJavascript/03.png)

Knockout is a MVVM framework created by Steve Sanderson at Microsoft on 2010. It’s using binding on declarative DOM. It can work with any web framework.
I’ve completed a simple introduction on this site. And it’s quite impressive. You have JavaScript intellisense if you use visual studio.

http://learn.knockoutjs.com/#/?tutorial=intro

![](./../../../assets/img/posts/2015-02-16-TechdaysEtatDeLieuxJavascript/04.png)

AngularJS is a JavaScript library created by Google on 2009. It’s a MVC framework to create Single Page Applications (SPA).
It supports two-way data binding, templates. You can use MVC, Ioc patterns. You can even create unit tests and integration tests.

![](./../../../assets/img/posts/2015-02-16-TechdaysEtatDeLieuxJavascript/05.png)

TypeScript is a programming language created by Microsoft on 2012. It can be transformed and compiled in JavaScript. And the generated JavaScript code supports multiple browsers. It can use interfaces and generics.

Grunt can compile TypeScript to JavaScript.

![](./../../../assets/img/posts/2015-02-16-TechdaysEtatDeLieuxJavascript/06.png)

Cordova is create by Apache on 2011.
Cordova is a set of device APIs that allow a mobile app developer to access native device function such as the camera or accelerometer from JavaScript. Combined with a UI framework such as jQuery Mobile or Dojo Mobile or Sencha Touch, this allows a smartphone app to be developed with just HTML, CSS, and JavaScript.
You can develop an application for multiple platform as Windows phone, IOS and Android without using CSharp, Objective-C, or Java.

The resume ends here. And you could choose appropriate technologies to build your web or mobile application.

![](./../../../assets/img/posts/2015-02-16-TechdaysEtatDeLieuxJavascript/07.png)

I hope you find this article helps!