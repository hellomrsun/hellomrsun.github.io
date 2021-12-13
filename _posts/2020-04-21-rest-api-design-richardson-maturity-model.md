---
layout: post
read_time: true
show_date: true
title:  REST API Design - Richardson Maturity Model
date:   2020-04-21 08:00:00 +0100
description: REST API Design - Richardson Maturity Model, WEB API
img: posts/uncategorized/open-api.png
tags: [REST, WebApi]
author: SUN Jiangong
---

Leonard Richardson has defined a Model to determine an REST API maturity, called **Richardson Maturity Model**.

There are 4 levels of maturity.

![](./../../../assets/img/posts/2020-04-21-RichardsonMaturityModel/richardson_maturity_model.png)

<br/>
<!--more-->

# LEVEL 0: THE SWAMP OF POX

<br/>

**The Swamp of POX** characteristics:

- the API exposes only **one** interface (or endpoint, or URI) which is used by **all types** of operations
- the method is **POST**
- the request and response messages are in plain old **XML** format
- the communication is in the form of **RPC** (Remote Procedure Call) over HTTP or **SOAP** (Simple Object Application Protocol) over HTTP

<br/>

# LEVEL 1: RESOURCES

<br/>

To improve the communication performance, multiple **URI**s (Unique Resource Identifier) are employed.

- one **specialized URI** treats one type of operation
- only one HTTP verb: **POST** is used for all types of operations

<br/>

# LEVEL 2: HTTP VERBS

<br/>

To improve the communication performance, multiple **URI**s (Unique Resource Identifier) are employed.

- one dedicated URI treats one type of operation
- different HTTP verbs are used: GET, POST, PUT, PATCH, DELETE
  * GET: Retrieve an item or a collection
  * POST: Create an item or a collection
  * PUT: Update an item (PUT is **idempotent** which means if an item already exists, PUT will replace it).
  * PATCH: Partial update on an item
  * DELETE: Delete an item or a collection

<br/>

# LEVEL 3: HYPERMEDIA CONTROLS

<br/>

Hypermedia controls provides HATEOAS (Hypermedia As The Engine Of Application State) on top of "HTTP Verbs".

It means the clients with previous little or no knowledge of the API, should be able to use it.

And HATEOAS make it possible in providing navigational links, relevant actions to describe the use cases of different resources in the API.

Here is a comparison between an API without HATEOAS and another API with HATEOAS.

With HATEOAS, you can see the **href**s and **method**s to be used to achieve the purpose of different **rel**s.

![](./../../../assets/img/posts/2020-04-21-RichardsonMaturityModel/rest_vs_hateoas_rest.png)

<br/>