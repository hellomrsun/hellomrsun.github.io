---
layout: post
title: REST API Design - Richardson Maturity Model
excerpt_separator:  <!--more-->
tags: REST API
canonical_url: 'https://sunjiangong.com/rest-api-design-richardson-maturity-model/'
---

Leonard Richardson has defined a Model to determine an REST API maturity, called **Richardson Maturity Model**.

There are 4 levels of maturity.

![](./../../../assets/images/RichardsonMaturityModel/richardson_maturity_model.png)

<!--more-->

<br/>

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

![](./../../../assets/images/RichardsonMaturityModel/rest_vs_hateoas_rest.png)

<br/>