---
layout: post
read_time: true
show_date: true
title:  How to traverse binary tree by breadth (Part II) ?
date:   2013-08-02 08:00:00 +0100
description: CSharp Algorithm - How to traverse binary tree by breadth (Part II)?
img: posts/uncategorized/algorithm.PNG
tags: [Algorithm]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-traverse-binary-tree-by-breadth-part-II.html'
---


Here I will introduce the breadth first traversal of binary tree.


The principe is that you traverse the binary tree level by level. 


This traversal is quite different than depth first traversal. In depth first traversal you can use recursive method to traverse.

<!--more-->

Here is one solution using a queue.

```csharp
/// <summary>
/// breadth-first traversal 宽度遍历树
/// </summary>
/// <typeparam name="T"></typeparam>
/// <param name="node"></param>
public void Traversal<T>(Node<T> node)
{
    //create a Node<T> queue
    var treeQueue = new Queue<Node<T>>();
    //initialize queue with tree root node
    treeQueue.Enqueue(node);

    //if queue has elements
    while (treeQueue.Count > 0)
    {
        //dequeue the queue's first node 
        Node<T> current = treeQueue.Dequeue();

        //print the node name
        PrintNodeName(current);
        
        //if node has Left leaf, enqueue it
        if (current.LNode != null)
            treeQueue.Enqueue(current.LNode);
        
        //if node has right leaf, enqueue it
        if (current.RNode != null)
            treeQueue.Enqueue(current.RNode);
    }
}
```