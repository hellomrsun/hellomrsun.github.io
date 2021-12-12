---
layout: post
# title: Conditional binding with trigger in WPF
# description: Conditional binding with trigger in WPF
# excerpt_separator:  <!--more-->
# tags: WPF
# canonical_url: 'https://sunjiangong.com/conditional-binding-with-trigger-in-wpf/'
read_time: true
show_date: true
title:  Conditional binding with trigger in WPF
date:   2015-02-25 08:00:00 +0100
description: Conditional binding with trigger in WPF, Windows Presentation Framework, CSharp, C#
img: posts/2015-02-25-wpf/wpf.PNG
tags: [WPF]
author: SUN Jiangong
# github:  hellomrsun
mathjax: yes
---

WPF conditional binding enables the application to have different behaviors based on a pre-defined condition.

For example, you could use conditional binding to change the background color of your WPF application main window.

Suppose you have the following window declaration in you WPF application.

<!--more-->

```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:views="clr-namespace:Views"
        xmlns:viewModels="clr-namespace:ViewModels"
        xmlns:controls="clr-namespace:Controls"
        Title="Main Application"
        Height="900"
        Width="1024"
        DataContext="{Binding Main, Source={StaticResource Locator}}">
```

You could add the following line in the window declaration :

```xml
Style="{DynamicResource ResourceKey=MainWindowStyle}"
```

And use the trigger to change the background color based on the binded property’s (EnvironmentIsSelected) value.

```xml
<Style TargetType="{x:Type Window}" x:Key="MainWindowStyle">
<Style.Triggers>
<DataTrigger Binding="{Binding Path=EnvironmentIsSelected}" Value="False">
<Setter Property="Background" Value="Pink"/>
</DataTrigger>
<DataTrigger Binding="{Binding Path=EnvironmentIsSelected}" Value="True">
<Setter Property="Background" Value="{Binding SelectedEnvironment.Color}"/>
</DataTrigger>
</Style.Triggers>
</Style>
```


I Hope you find this article helpful!

