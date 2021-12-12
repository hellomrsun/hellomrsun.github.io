---
layout: post
# title: How to create custom snippet in Visual Studio
# description: How to create custom snippet in Visual Studio
# excerpt_separator:  <!--more-->
# tags: Visual-Studio
# canonical_url: 'https://sunjiangong.com/how-to-create-custom-snippet-in-visual-studio/'
read_time: true
show_date: true
title:  How to create custom snippet in Visual Studio?
date:   2014-01-23 08:00:00 +0100
description: How to create custom snippet in Visual Studio? CSharp, C#
img: posts/uncategorized/Visual-Studio.png
tags: [VisualStudio]
author: SUN Jiangong
# github:  hellomrsun
mathjax: yes
---


To improve the programming productivity, you can your personal snippet in visual studio. If the work occurs repeatly, the snippet can dramatically reduce your time.

Here I'll introduce to you how to do it. :)

<!--more-->

Firstly create a snippet file for copyright.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>copyright</Title>
      <Shortcut>cr</Shortcut>
      <Description>Code snippet for copyright notice</Description>
      <Author>author name</Author>
      <SnippetTypes>
        <SnippetType>Expansion</SnippetType>
      </SnippetTypes>
    </Header>
    <Snippet>
      <Declarations>
		<Literal Editable="false">
			<ID>classname</ID>
			<ToolTip>Class name</ToolTip>
			<Function>ClassName()</Function>
			<Default>ClassNamePlaceholder</Default>
		</Literal>
      </Declarations>
      <Code Language="csharp">
        <![CDATA[// --------------------------------------------------------------------------
                // <copyright file="$classname$.cs" company="My company">
                //   2013
                // </copyright>
                // <summary>
                //   The $classname$ class.
                // </summary>
                // -----------------------------------------------------------------------------------
      ]]>
      </Code>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
```

Then import your snippet to visual studio.


Goto : Tools -> Code Snippet Manager -> Import. Choose your snippet file and import it.


Then, you can use the snippet in your visual studio. 


Enjoy coding!

