---
layout: post
read_time: true
show_date: true
title:  A little thought about .NET Framework, CTS, CLI, CLS, CLR and C#
date:   2013-07-11 08:00:00 +0100
description: A little thought about .NET Framework, CTS, CLI, CLS, CLR and C#, Csharp, Dotnet framework, Microsoft
img: posts/uncategorized/csharp.jpg
tags: [DotNet]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/a-little-thought-about-dotnet-framework-cts-cli-cls-clr-csharp.html'
---

#### Terms:

CTS: Common Type Specification

CLI: Common Language Infrastructure

CLS: Common Language Specification

CLR: Common Language Runtime

JIT: Just In Time 

CIL: Common Intermediate Language

MSIL: MicroSoft Intermediate Language 

VES: Virtual Execution System

NGEN: Native image GENerator

FCL: Framework Class Library

BCL: Base Class Library

<br />
<!--more-->

#### Relationships: 

CLR  <==> VES <==> JVM in Java

Managed code <==> MSIL <==> CIL

Unmanaged code <==> native code <==> machine code

<br />

#### CLI:

CLR, CTS, CLS and metadata specification are all parts of CLI.

CTS: Microsoft introduces CTS to intercommunicate among data types in different programming languages.

CLS: It defines rules that all .NET languages should respect, and it's part of CTS.

CLR is the Microsoft implementation of VES. 

CLR contains: Garbage collector for automatic memory management, JIT for compilation from CIL to native code, Type checker, Debug engine, Security engine, Class loader, Thread support, Exception manager, Com marshaler.

<br />

Computers can only understand machine code.

Machine code is a sequence of binary (1 and 0).

<br />

#### Compiled language vs Interpreted language:

C# is a compiled language, because it's compiled to CIL, and then it's interpreted by JIT to machine code.

The difference between compiled language and interpreted language is: Interpreted language will be executed by interpretor, line by line on local machine.

<br />

##### Compiled language:

More rapid execution speed, because it’s already compiledand targeted to local machine

Less memory usage, because it’s compiled

<br />

##### Interpreted language:

Independent platform, because it doesn’t need to be compiled

Code size is smaller than compiled code

<br />

.NET Framework: consists of Common Language Runtime and Class Library. 


#### C# source code execution steps:

C# source code --C# Compiler(csc.exe) --> CIL/MSIL (managed code/ byte code) stores in assemblies like DLL or EXE --JIT in CLR or NGEN--> native code (unmanaged/machine code) --> Execution

<br />

#### Difference between managed code and native code/machine code/unmanaged code:

##### Managed code:

Code compiled by C# sharp compiler is called managed code, it's stored in assemblies like DLL or EXE files.

Managed code is the intermediate code between source code and native code. Managed code is CPU independent code.

MSIL must be converted to CPU-specific code which is machine code to be run, it will be compiled by JIT compiler in CLR at runtime.

CLR supplies one or more JIT compilers for each computer architecture it supports, the same set of MSIL can be JIT-compiled and run on any supported architecture.

<br />

##### Native code:

Native code runs straight on the CPU. They are machine code targeted towards a specific architecture (for instance, Intel's x86). It'sCPU-Specific code.

Native code is the code whose memory is not "managed". There is no reference counting, no garbage collection.

<br />

#### Assembly

Assembly contains metadata type, assembly manifest who contains assembly metadata, CIL, and resources.

Metadata is data describes the states of assembly and a detailed description of each type and attribute in application.

Metadata contains: 

- Descriptions of assembly: Identity (Name, version, culture, public key), the types that are exported, other assemblies that the assembly depends on, security permissions needed to run.

- Description of types: Name, visibility, base class, and interfaces implemented, members (methods, fields, properties, events, nested types)

- Attributes: additional descriptive elements 

<br />

#### Difference between JIT and NGEN:

The Native Image Generator (Ngen.exe) is a tool that improves the performance of managed applications. 

Ngen.exe creates native images, which are files containing compiled processor-specific machine code, and installs them into the native image cache on the local computer. The runtime can use native images from the cache instead of using the just-in-time (JIT) compiler to compile the original assembly.
