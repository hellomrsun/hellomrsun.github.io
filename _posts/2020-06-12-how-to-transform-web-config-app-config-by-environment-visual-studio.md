---
layout: post
read_time: true
show_date: true
title:  How to transform web config or app config by environment in visual studio
date:   2020-06-12 08:00:00 +0100
description: How to transform web config or app config by environment in visual studio
img: posts/2020-06-12-NetFrameworkConfigTransform/00_download.PNG
tags: [DevOps, MsBuild, VisualStudio, ConfigurationTransform]
author: SUN Jiangong
mathjax: yes
redirect_from:
  - /2020/06/12/how-to-manage-app-config-by-environment.html
---

In software development, there are at least several environments to manage: development (DEV), staging (STAG or PRE), and production (PRD). 

There will be integration (INT), user acceptance testing (UAT) in a more complete environment configuration.

It could be frustrating when managing all those environments because a small error in the deployment could generate an incident, or disaster!

Fortunately there is a cool tool to facilitate the environment management and software deployment in visual studio.

<!--more-->

It is a visual studio extension: **Configuration Transform**

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/00_download.PNG)


Once you have installed Configuration Transform, you can create environment configurations for your project.

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/01_add_profiles.PNG)

And then you can location the **app.config**, right click on it and then choose **Add config transforms**.

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/02_generate.png)

You can see the following configuration files for DEV and INT.

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/03_configs.png)

Now, I have prepared some code to ensure the correct config file is used when running the program.

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/04_code.png)

And with the App.config:

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/05_default_config.png)

To override the default configuration for INT environment, **ApplicationName** is replaced in **App.INT.config**.

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/06_transform_replace.png)

The following MSBuild command will build the solution, and generate the binaries with the correct App.config.

```bash
> MSBuild.exe NetDemo.sln /property:Configuration=INT -target:clean;compile;build
```

You can see App.INT.config is used to replace the default configuration of App.config, and generate the final **NetDemo.exe.config**.

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/07_build_detail.png)


You can see the ApplicationName is "NetDemo INT" when the program run.

![](./../../../assets/img/posts/2020-06-12-NetFrameworkConfigTransform/08_run.png)

You can download the source code [HERE](https://github.com/hellomrsun/BlogCodeSource/tree/master/src/2020-06-11_Configuration_Transform)