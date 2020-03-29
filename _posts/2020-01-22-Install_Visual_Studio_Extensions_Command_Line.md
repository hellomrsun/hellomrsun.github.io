---
layout: post
title: How to install Visual Studio Extensions in Command Line?
author: SUN Jiangong
excerpt_separator:  <!--more-->
tags: Visual-Studio
canonical_url: 'https://sunjiangong.com/How-to-install-Visual-Studio-Extensions-in-Command-Line/'
---

If you have limited user right and you are not able to install some Visual Studio Extensions (.VSIX) directly, you can install them in command line.

<!--more-->

1. Firstly, you can download the extension in [Visual Studio MarketPlace](https://marketplace.visualstudio.com).

2. Launch CMD.exe with highest user right profile you have.

3. Then, go to correct Visual Studio IDE folder.

For example, The folder is "C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE" for Visual Studio 2017 Community version.

Beware of the Visual Studio folder will be different depending its version.

| Visual Studio Version | Visual Studio Internal Version | Physical folder |
| --- | --- | -- |
| VS 2012 | VS 11.0 | C:\Program Files (x86)\Microsoft Visual Studio 11.0 |
| VS 2013 | VS 12.0 | C:\Program Files (x86)\Microsoft Visual Studio 12.0 |
| VS 2015 | VS 14.0 | C:\Program Files (x86)\Microsoft Visual Studio 14.0 |
| VS 2017 | VS 15.0 | C:\Program Files (x86)\Microsoft Visual Studio\2017 |

4. Execute the command:

```
> VSIXInstaller.exe /quiet /admin "VSIX_File_Path"
```
or
```
> VSIXInstaller.exe /q /a "VSIX_File_Path"
```


