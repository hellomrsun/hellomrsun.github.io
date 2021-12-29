---
layout: post
read_time: true
show_date: true
title:  Some notes about DOM (Document Object Model)
date:   2010-01-03 13:32:20 +0100
description: Some notes about DOM (Document Object Model)
img: posts/2021-01-03-DOM/window-dom.PNG 
tags: [DOM]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/some-notes-on-document-object-model.html'
mathjax: yes
---


I have read a good introduction article about DOM (Document Object Model):

The purpose of this assignment was to learn how to use JavaScript with the DOM(Document Object Model), and about some of the properties available through the DOM's window object.

The description and my solution of the DOM Properties-assignment can be viewed at the bottom of this page.

<!--more-->

##### What is DOM

The DOM is an API for HTML and XML documents.

It defines the structure of documents and the way to access that structure in favor for manipulating how the document will be presented, what the document's content will be and how the document will be structured.

With this model programmers can create documents, navigate the document, add, change or delete elements and content.

A very common script language using DOM as a model is JavaScript. However, the model itself has noting to do with JavaScript, it is simply a model that can be used by any programming language or scripting language.

Care must be taken when using the DOM since many browsing software offer extensions not following the W3C standard.

What is the DOM Window Object?

The window object represents the window itself. It is created automatically with every instance of a <body> or <frameset> tag. The window object contains the document as a child and provides - among others objects - access to the useful window.navigator and window.screen objects. These two objects are often used for manipulating the browsing environment itself, and provides many special properties for accessing objects futher down the tree structure.


Assignment Description

Create a Web page with functionality for displaying the different properties of the window, window.screen, window.navigator window.location, window.history and window.document objects.


Basic object model for all modern browsers:


![](./../../../assets/img/posts/2021-01-03-DOM/window-dom.PNG)

 

About typeof:

 

typeof returns one of the following strings :
number
string
boolean
object
function
undefined (= null )
typeof(typeof(x)) is always string , no matter what x actually is.
IE seems to think that some functions are objects rather than functions: typeof(document.getElementById) returns object.
 

I have done a testing code about all the objects in DOM, it concerns all the properties of all the objects.

Here is the code:

```html
<html>
<head>
<title>All the DOM objects</title>
<script type="text/javascript">
function showBrowserType() {
document.getElementById("readout").innerHTML = navigator.userAgent+"! "+navigator.appName+"! "+navigator.appCodeName+"! "+navigator.appVersion+"! "+ navigator.cookieEnabled+"! "+navigator.platform+"!";

document.getElementById("window").innerHTML = window.name+"! "+window.defaultStatus+"! "+window.status+"! "+window.opener+"! "+window.parent+"! "+window.top+"! "+window.closed+"! ";

//等价于
document.getElementById("window").innerHTML = name+"! "+status+"! "+opener+"!"+parent+"! "+top+"!"+closed+"! "+defaultStatus+"! ";
document.getElementById("screen").innerHTML = screen.width+"! "+screen.height+"! "+screen.colorDepth+"! "+screen.availableWidth+"! "+screen.availableHeight+"! ";
document.getElementById("location").innerHTML = location.href+"! "+location.protocol+"! "+location.hostname+"! "+location.host+"! "+location.port+"! "+location.pathname+"! "+location.hash+"! "+location.search+"! ";
document.getElementById("history").innerHTML = history.length+"! ";
document.getElementById("document").innerHTML = document.cookie+"! "+document.referer+"! "+document.domain+"! "+document.lastModified+"! ";
}
window.onload = showBrowserType;
</script>
</head>
<body>
<div id="readout" style="background-color:green"></div><br/><br/>
<div id="window" style="background-color:blue"></div><br/><br/>
<div id="screen" style="background-color:yellow"></div><br/><br/>
<div id="location" style="background-color:red"></div><br/><br/>
<div id="history" style="background-color:orange"></div><br/><br/>
<div id="document" style="background-color:clay"></div><br/>
</body>
</html>
```