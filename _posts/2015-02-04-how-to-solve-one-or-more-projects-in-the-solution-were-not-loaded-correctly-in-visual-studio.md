---
layout: post
read_time: true
show_date: true
title:  How to solve one or more projects in the solution were not loaded correctly error in visual studio?
date:   2015-02-04 08:00:00 +0100
description: How to solve one or more projects in the solution were not loaded correctly error in visual studio?
img: posts/uncategorized/Visual-Studio.png
tags: [VisualStudio]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-solve-one-or-more-projects-in-the-solution-were-not-loaded-correctly-in-visual-studio.html'
---


When building an enterprise application, there could have a lot of projects in one solution. And several developers create new projects to meet the business requirement. And also some re-factorization could be undertaking at the same time. The re-factorization could be varied, such as rename the projects and reorganize project folders or combine some projects into one project etc.

Some inconsistency problem may occur in your solution file during the developing & refactoring process.
 
The has happened in my project solution, which contains more than 100 projects (Tools, Web Services, Windows Services, Common Libraries, Integration tests, Unit tests). While this solution needs to be splited to be more readble. This is another history.

<!--more-->

So every time I open the product solution, I have a warning : 

```bash
one or more projects in the solution were not loaded correctly please see the output
```

And then I check the output, I have the message :

```bash
some of the properties associated with the solution could not be read.
```

When I check the solution(.sln) file. The "SccNumberOfProjects" has occurred twice whereas the number of this property is not the same, which causes the solution load warning.

So what you need to do is just modify it with correct project numbers. And then the problem is solved!
