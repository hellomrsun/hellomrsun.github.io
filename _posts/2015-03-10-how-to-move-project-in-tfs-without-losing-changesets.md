---
layout: post
read_time: true
show_date: true
title:  How to move project in TFS without losing changesets
date:   2015-03-10 08:00:00 +0100
description: How to move project in TFS without losing changesets, Team foundation server
img: posts/uncategorized/tfs.png
tags: [TFS]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-move-project-in-tfs-without-losing-changesets.html'
---

There are something you need to pay attention to when you make a project move refactoring.

You could NEVER delete a project in the TFS and re-add it into the place you want. In this way, you will lose all the changesets about this project.

What you should do is move the project to another place with TFS.

<!--more-->

Firstly, click add button to create a new folder in TFS source control explorer.

![](./../../../assets/img/posts/2015-03-10-TFSMoveProject/01.png)

You will see the green button on the left once you have successfully created a new folder. And it’s marked as “Add”.

![](./../../../assets/img/posts/2015-03-10-TFSMoveProject/02.png)

Then, Move your project to the new folder.
Right click your project, then click “Move”

![](./../../../assets/img/posts/2015-03-10-TFSMoveProject/03.png)

TFS will propose you for the destination folder. Just specify the folder you have created.

![](./../../../assets/img/posts/2015-03-10-TFSMoveProject/04.png)

When you have done all the previous steps, you could check-in your modifications. And TFS will link all the project changeset histories to the new folder.

I hope you find this articile helpful!