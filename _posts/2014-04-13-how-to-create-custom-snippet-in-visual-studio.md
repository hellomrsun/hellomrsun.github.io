---
layout: post
read_time: true
show_date: true
title:  How to create custom snippet in Visual studio?
date:   2014-04-13 08:00:00 +0100
description: How to create custom snippet in Visual studio?
img: posts/uncategorized/Visual-Studio.png
tags: [VisualStudio]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-create-custom-snippet-in-visual-studio.html'
---


To improve the programming productivity, you can your personal snippet in visual studio. If the work occurs repeatly, the snippet can dramatically reduce your time.

Here I'll introduce to you how to do it. :)


Firstly create a snippet file for copyright.

```csharp
<?xml version="1.0" encoding="utf-8" ?>
<CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>copyright</Title>
      <Shortcut>cr</Shortcut>
      <Description>Code snippet for copyright notice</Description>
      <Author>SUN Jiangong</Author>
      <SnippetTypes>
        <SnippetType>Expansion</SnippetType>
      </SnippetTypes>
    </Header>
    <Snippet>
      <Declarations>
		<Literal Editable="true">
			<ID>classname</ID>
			<ToolTip>Class name</ToolTip>
			<Function>ClassName()</Function>
			<Default>ClassNamePlaceholder</Default>
		</Literal>
      </Declarations>
      <Code Language="csharp">
        <![CDATA[
                // --------------------------------------------------------------------------
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


Go to : Tools -> Code Snippet Manager -> Import. or Press Ctrl+K, then Ctrl+B.

Choose your snippet file and import it.

Then, you can use the snippet in your visual studio. 


Enjoy coding!
