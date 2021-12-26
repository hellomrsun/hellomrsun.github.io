---
layout: post
read_time: true
show_date: true
title:  How to traverse binary tree by depth (Part I) ?
date:   2013-07-10 08:00:00 +0100
description: How to traverse binary tree by depth (Part I), csharp, algorithm
img: posts/uncategorized/algorithm.PNG
tags: [CSharp, Algorithm]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/how-to-traverse-binary-tree-by-depth.html'
---

In this article, I will introduce the traversal of binary tree in CSharp.

There are depth first traversal which includes: 

- pre-order traversal: root node first, then left node, then right node

- in-order traversal: left node first, then root node, then right node

- post-order traversal: left node first, then right node, then root node

and breath first traversal which is level-order traversal.

<!--more-->

In this post I will introduce the depth first traversal, and later for breath first traversal.


So, before we traverse a binary tree, we need to create it before. And before we create a tree, we need to create tree node. I assume the data hold the value, and the left node and right node are its children.


```csharp
public class Node<T>
{
    public Node<T> LNode { get; set; }
    public Node<T> RNode { get; set; }
    public T Data { get; set; }
    public Node(T data)
    {
        Data = data;
    }
}
```

Then, I need to create a binary tree.

```csharp
static Node<string> BinTree()
{
    Node<string>[] binTree = new Node<string>[11];
    binTree[0] = new Node<string>("A");
    binTree[1] = new Node<string>("B");
    binTree[2] = new Node<string>("C");
    binTree[3] = new Node<string>("D");
    binTree[4] = new Node<string>("E");
    binTree[5] = new Node<string>("F");
    binTree[6] = new Node<string>("G");
    binTree[7] = new Node<string>("H");
    binTree[8] = new Node<string>("I");
    binTree[9] = new Node<string>("J");
    binTree[10] = new Node<string>("K");

    binTree[0].LNode = binTree[1];
    binTree[0].RNode = binTree[2];
    binTree[1].LNode = binTree[3];
    binTree[1].RNode = binTree[4];
    binTree[2].LNode = binTree[5];
    binTree[2].RNode = binTree[6];
    binTree[3].RNode = binTree[7];
    binTree[4].LNode = binTree[8];
    binTree[5].LNode = binTree[9];
    binTree[5].RNode = binTree[10];
    return binTree[0];
}
```

Once I have the tree, I can think about creating the different binary tree traversals.
Firstly, let's see the pre-order traversal. 

The principe is the we get the root value, then its left node value and finally its right node value.

**Remember**: Left node is always before Right node.


```csharp
static void PreOrder<T>(Node<T> node)
{
    if (node != null)
    {
        Console.WriteLine(node.Data);
        PreOrder<T>(node.LNode);
        PreOrder<T>(node.RNode);
    }
}
```

In the previous method, we've used recursive method to get the node's child, and its child's child etc.

Then, we can see the in-order traversal. It just change the order of the three nodes.

The principe is the we get the its left node value, then root value, and finally its right node value.

```csharp
static void InOrder<T>(Node<T> node)
{
    if (node != null)
    {
        PreOrder<T>(node.LNode);
        Console.WriteLine(node.Data);
        PreOrder<T>(node.RNode);
    }
}
```

Finally, the post-order traversal.
The principe is the we get the its left node value, then its right node value, and finally its root value.

```csharp
static void PostOrder<T>(Node<T> node)
{
    if (node != null)
    {
        PreOrder<T>(node.LNode);
        PreOrder<T>(node.RNode);
        Console.WriteLine(node.Data);
    }
}
```

Now, we just need to call the different implementations and get the results.

```csharp
public static void Main()
{
    Node<string> tree = BinTree();
    PreOrder<string>(tree); //result: A B D H E I C F J K G
    InOrder(tree); //result: B D H E I A C F J K G
    PostOrder<string>(tree); //result: B D H E I C F J K G A

    Console.ReadKey();
}
```

So here, we've arrived at the end of this post, I hope this does help to you. Enjoy coding!
