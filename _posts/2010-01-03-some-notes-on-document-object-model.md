---
layout: post
title: Some notes about DOM (Document Object Model)
description: Some notes about DOM (Document Object Model)
excerpt_separator:  <!--more-->
tags: HTML | DOM
canonical_url: 'https://sunjiangong.com/IIS-configuration-with-support-of-multiple-domain-urls/'
---


I have read a good introduction article about DOM (Document Object Model):

The purpose of this assignment was to learn how to use JavaScript with the DOM(Document Object Model), and about some of the properties available through the DOM's window object.

The description and my solution of the DOM Properties-assignment can be viewed at the bottom of this page.


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
 

Original Address:  http://www.webpelican.com/internet-programming-3/dom-properties/

dom Structure see:  http://www.howtocreate.co.uk/tutorials/javascript/domstructure

 
Basic object model for all modern browsers:


![](./../../../assets/images/2021-01-03-DOM/window-dom.PNG)

 

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

