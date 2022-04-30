---
layout: post
read_time: true
show_date: true
title:  Microsoft Techdays Paris 2013 - Day 3
date:   2013-03-28 08:00:00 +0100
description: Microsoft Techdays Paris 2013 - Day 3
img: posts/uncategorized/microsoft.png
tags: [TechEvents]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/microsoft-techdays-paris-2013-day-3.html'
---

Finally, my third post about MS Techdays Paris comes! I've prefered to pay attention to sharepoint and WPF on the last day. And two of four sessions I've participated were about SharePoint, one about WPF and another one about Continuous integration.

Here we go!

<!--more-->

### Session 1: Fier d'être developpeur office & SharePoint(Microsoft)


- SharePoint 2013 new features:

App model, CSR, Design manager, REST/Client side object model, JsLink, Server side , Display template, workflows, Access

- Apps for office:

"Napa" office 365 development tools

- office apps type: 
    - task pane(for word, excel, ppt, project)
    - content app(for excel)
    - mail app(for outlook)

App for office 365: No need to develop in C#(unique in web)

4 important files for an app: html, css, js, xml

- SharePoint app types
    - 1 fullpage: complete pages
    - 2 app parts: addable "web parts" in sharepoint website pages
    App parts is Iframe, it exchanges properties and query string
        - 2.1 Cloud hosted app
            - 2.1.1 provider hosted app(IIS, apache)
            - 2.1.2 auto hosted app(Windows AZure + Sql AZure)
        - 2.2 Sharepoint hosted app: 100% sharepoint, with a lot of javascript code but without c#
            App package: file type is .app
            package repository: Images, CSS, Pages, Scripts
    - 3 UI command extensions: extensions for menus

- CSR(Client Side Rendering)
    - SharePoint 2007 -> CAML
    - SharePoint 2010 -> XSL
    - SharePoint 2013 -> CSR


### Session 2: Convevoir & valider l'archtecture WPF modulaire (Amadeus)

1 billion travel transactions everyday treated by the data center.

Architecture: WPF, Prism V4, WCF

Prism is a mvvm pattern framework

MVVM : separate UI and Logic layer; binding principe; test facility

- complex and modular architecture
- community development
- high performance
- high quality of code

3 layers:
- 1) UI (View - commands)
- 2) Core (Business logic - actions)
- 3) DAL (services - message)

Most used UML diagrams: 
- Class diagram(for reverse engineering) 
- Sequence diagram(for refactoring)

In Architecture explorer -> Add class to uml diagram (diagram will be generated automatically)

Code clone: new feature in VS 2012

VS 2012 -> Menu -> Analyse solution for code clone


### Session 3: ITIL: ALM, un jour, votre application sera en production (Microsoft, Amettis, Exakis)

A shortened development life cycle:

![](./../../../assets/img/posts/2013-03-28-techdays-day-3/1.png)

ITIL : service life cycle

![](./../../../assets/img/posts/2013-03-28-techdays-day-3/2.png)

### Session 4: Adoption utilisateurs, controle et comprehension documentaire pour tous(Kodak)

GED: Gestion de electronique documentaire is used in SharePoint 2010 and SharePoint 2013

- SharePoint 2003 -> share documents
- SharePoint 2007 -> collaboration
- SharePoint 2010 -> content management (Content organizer, document ID)
- SharePoint 2013 -> cloud, social mobile (AppStore, Enhanced Search)

Capture: who, what, when, where, why?

Indexer: extract the documents data

Workflow: control the data flow

### Session 5: Intégration continue chez AXA France

Continuous Deployment:
- 1 deploy intallation on one or more virtual machines in the end of the build; 
- 2 execute integration tests

Benefit: 
- 1 better monitoring of archive problems
- 2 monitoring quality indicator
- 3 continuous demonstration

I hope this post can do help!
