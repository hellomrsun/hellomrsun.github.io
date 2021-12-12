---
layout: post
read_time: true
show_date: true
title:  Some useful resources in developing websites with Angular
date:   2020-03-19 08:00:00 +0100
description: Some useful resources in developing websites with Angular
img: posts/2020-03-19-AngularStarter/AngularUIFrameworks.png
tags: [Angular]
author: SUN Jiangong
mathjax: yes
---

I would like to share some useful tips in developing web applications with Angular.

<!-- TOC -->

- [Part 1 : UI Frameworks](#part-1--ui-frameworks)
- [Part 2: Extensions](#part-2-extensions)
  - [Angular Follow Selector](#angular-follow-selector)
  - [Angular Language Service](#angular-language-service)
  - [Debugger for Chrome](#debugger-for-chrome)
  - [ESLint or TSLint](#eslint-or-tslint)
  - [Angular Essentials (Version 9)](#angular-essentials-version-9)
- [Part 3. Coding](#part-3-coding)

<!-- /TOC -->

<!--more-->

### Part 1 : UI Frameworks

To kick off an Angular project, you can use some Angular UI Libraries, like: [Angular Material](https://material.angular.io/), [PrimeNG](https://www.primefaces.org/primeng/), [NG-Zorro](https://ng.ant.design/) and other UI frameworks.

Here is a list of UI frameworks that Angular recommend:

![](./../../../assets/img/posts/2020-03-19-AngularStarter/AngularUIFrameworks.png)

Source: [Angular Development Resources](https://angular.io/resources?category=development)

<br/>

### Part 2: Extensions

For those who develop Angular web applications in Visual Studio Code, there are some very useful extensions you can not miss.

#### [Angular Follow Selector](https://marketplace.visualstudio.com/items?itemName=sanderledegen.angular-follow-selector)

![](./../../../assets/img/posts/2020-03-19-AngularStarter/angular-follow-selector.gif)

<br/>

#### [Angular Language Service](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)

![](./../../../assets/img/posts/2020-03-19-AngularStarter/AngularLanguageService.gif)

<br/>

#### [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)

![](./../../../assets/img/posts/2020-03-19-AngularStarter/DebuggerForChrome.gif)

To debug correctly in Angular >= 6, you can follow this configuration in launch.json:
```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "ng serve",
      "type": "chrome",
      "request": "launch",
      "preLaunchTask": "npm: start",
      "url": "http://localhost:4200/#",
      "webRoot": "${workspaceFolder}",
      "sourceMapPathOverrides": {
        "webpack:/*": "${webRoot}/*",
        "/./*": "${webRoot}/*",
        "/src/*": "${webRoot}/*",
        "/*": "*",
        "/./~/*": "${webRoot}/node_modules/*"
      }
    },
    {
      "name": "ng test",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:9876/debug.html",
      "webRoot": "${workspaceFolder}",
      "sourceMaps": true,
      "sourceMapPathOverrides": {
        "webpack:/*": "${webRoot}/*",
        "/./*": "${webRoot}/*",
        "/src/*": "${webRoot}/*",
        "/*": "*",
        "/./~/*": "${webRoot}/node_modules/*"
      }
    },
    {
      "name": "ng e2e",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/protractor/bin/protractor",
      "protocol": "inspector",
      "args": [
        "${workspaceFolder}/e2e/protractor.conf.js"
      ]
    }
  ]
}
```

For more details, check [Angular CLI Debug](https://github.com/microsoft/vscode-recipes/tree/master/Angular-CLI)

<br/>

#### ESLint or TSLint

[ESLint](https://eslint.org/)

[ESLint Exension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

[TSLint](https://palantir.github.io/tslint/)

[TSLint Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-typescript-tslint-plugin)


<br/>

#### [Angular Essentials (Version 9)](https://marketplace.visualstudio.com/items?itemName=johnpapa.angular-essentials)


![](./../../../assets/img/posts/2020-03-19-AngularStarter/AngularEssentials.PNG)

<br/>

### Part 3. Coding

[Angular Coding style guide](https://angular.io/guide/styleguide)
