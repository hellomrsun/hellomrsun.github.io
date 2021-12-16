---
layout: post
read_time: true
show_date: true
title:  How to unshelve a shelveset into another branch with TFS?
date:   2014-05-21 08:00:00 +0100
description: How to unshelve a shelveset into another branch with TFS? Team Foundation Server, DevOps
img: posts/uncategorized/tfs.png
tags: [TFS]
author: SUN Jiangong
mathjax: yes
redirect_from:
  - /2014/05/21/how-to-unshelve-a-shelveset-into-another-branch-with-tfs.html
---

If you have made a shelve in one branch, and want to unshelve it to another branch. 

This article will be helpful for you.

There are some steps to follow:

#### 1. You need to install TFS Power tools in your machine. Or else, you can't use tfpt command.

#### 2. You need to ensure there is no pending changes in all branches in the workspace. 

If not, you may get possible errors like:
- Unable to determine the workspace
- An item with the same key has already been added

<!--more-->

#### 3. And it's better to delete cache in TFS: C:\Users[USERNAME]\AppData\Local\Microsoft\Team Foundation\4.0\Cache

#### 4. Go to the target branch name

Example : 

```batch
c:\>d:
d:\>cd D:\wks\XXX\LOCAL_TARGET_BRANCH
```

#### 5. Run tfpt unshelve command in target branch mapped directory

Example:

```batch
D:\wks\XXX\LOCAL_TARGET_BRANCH>tfpt unshelve /migrate "SourceBranchShelveName" /source:"$/PATH/SOURCE_BRANCH" /target:"$/PATH/TARGET_BRANCH" 
```

#### 6. Resolve conflicts

There may have some conflicts in the unselve, you can choose auto merge all or resolve the conflicts one by one.


Hope this helps! Enjoy coding!




**References:**

http://geekswithblogs.net/TarunArora/archive/2011/06/06/unshelve-shelveset-created-from-one-branch-to-another.aspx

http://benjii.me/2014/04/move-shelveset-to-different-branch-in-tfs/




