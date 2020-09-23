---
layout: post
title: Move project in TFS without losing changesets
description: Move project in TFS without losing changesets
excerpt_separator:  <!--more-->
tags: TFS
canonical_url: 'https://sunjiangong.com/move-project-in-tfs-without-losing-changesets/'
---

There are something you need to pay attention to when you make a project move refactoring.

You could NEVER delete a project in the TFS and re-add it into the place you want. In this way, you will lose all the changesets about this project.

<!--more-->

What you should do is move the project to another place with TFS.

Firstly, click add button to create a new folder in TFS source control explorer.

![](./../../../assets/images/TFSMoveProject/01.png)

You will see the green button on the left once you have successfully created a new folder. And it’s marked as “Add”.

![](./../../../assets/images/TFSMoveProject/02.png)

Then, Move your project to the new folder.
Right click your project, then click “Move”

![](./../../../assets/images/TFSMoveProject/03.png)

TFS will propose you for the destination folder. Just specify the folder you have created.

![](./../../../assets/images/TFSMoveProject/04.png)

When you have done all the previous steps, you could check-in your modifications. And TFS will link all the project changeset histories to the new folder.

I hope you find this articile helpful!