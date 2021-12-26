---
layout: post
read_time: true
show_date: true
title:  Code refactoring - bad smells in code and refactoring techniques
date:   2013-06-05 08:00:00 +0100
description: Code refactoring - bad smells in code and refactoring techniques
img: posts/uncategorized/craftsman.PNG
tags: [Craftsmanship]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/code-refactoring-bad-smells-in-code-and-refactoring-techniques.html'
---

There is a list of refactoring techniques with examples.


- Duplicated code

Extract method or Extract class

- Long method

Extract method, Inline method, replace temp variable by query, Parameter object(DTO), Replace method by method object

<!--more-->

- Large class

Extract class, extract subclass, 

- Long parameter list

Preserve whole object, Introduce parameter object

- Divergent change发散式变化

Extract class: divide class into different sub classes, in this way, several changes in a class can be made into several sub classes.

- Shortgun surgery 霰弹修改; 和发散式变化正相反

Move method, move field: put all codes need to be modified into a class for preventing from forgetness in a lot of differenct classes. 

- Feature Envy 依恋情结

symptom: a method use a lot of method in another class.

Move method, Strategy, Visitor pattern

- Data clumps 数据泥团

- Primitive obsession 基本类型偏执

Replace data value with object, replace type code with class

- Switch statements : switch 惊悚现身

Replace conditional with polymorphism

- Parallel inheritance hierarchies 平行继承体系

symptom: when you create a subclass for a class, you have to create a subclass for another class.

solution: make sure that instances of one hierarchy refer to instances of the other

- Lazy class冗赘类

symptom: a class is not doing a lot of work

solution: inline class, means moving all it's features into another class.

- speculative generality 夸夸其谈未来性

remove parameter, collapse hierarchy, inline class

- temporary field 暂时字段

extract class, introduce nullable object

- message chains过度耦合的信息链

symptom: You see message chains when a client asks one object for another object, which the client then asks for yet another object, which the client then asks for yet another another object, and so on.
solution: hide delegate

- middle man 中间人

delegate

- inappropriate intimacy 不合适的亲昵行为

extract method, extract class


- alternative classes with different interfaces 


- incomplete library class


- data class


- refused requests

- comments

Extract method, Rename method

