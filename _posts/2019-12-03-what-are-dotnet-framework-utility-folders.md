---
layout: post
# title: .Net framework utility folders
# description: DotNet Framework, Microsoft SDK, Visual studio utility folder
# excerpt_separator:  <!--more-->
# tags: DotNet-Utility
# canonical_url: 'https://sunjiangong.com/what-are-dotnet-framework-utility-folders/'
read_time: true
show_date: true
title:  .Net framework utility folders
date:   2019-12-03 08:00:00 +0100
description: .Net framework utility folders, DotNet Framework, Microsoft SDK, Visual studio utility folder
img: posts/2019-dotnet-framework/dotnet.jpg
tags: [DotNet]
author: SUN Jiangong
# github:  hellomrsun
mathjax: yes
---

As a .NET developer, there are some utility folders you might need to use in your development, build, debugging, test, and deployment, etc.
And .NET framework and Visual studio do provide a lot of tools.

For example, I can use WcfTestClient.exe to test a WCF service endpoint.
But I always forget its folder, and end up by searching it on Google or StackOverFlow.
So, here I summarize the most frequently used utility folders in .NET development.


<!--more-->

<br/>

- [1. DotNet Framework folder](#1-dotnet-framework-folder)
- [2. Microsoft SDK folder](#2-microsoft-sdk-folder)
- [3. Visual Studio folder](#3-visual-studio-folder)
- [4. .NET Core SDK Folder](#4-net-core-sdk-folder)

<br/>

#### 1. DotNet Framework folder ####

`C:\Windows\Microsoft.NET`

Folder structure:

* Assembly
  * GAC_32
  * GAC_64
  * GAC_MSIL
* Framework
  * v1.0.3705
  * v1.1.4322
  * v2.0.50727
  * v3.0
  * v3.5
  * v4.0.30319
    * <b>csc.exe</b>: CSharp Compiler
    * <b>vbc.exe</b>: Visual Basic Compiler
    * <b>clr.dll</b>: CLR engine
    * <b>clrjit.dll</b>: CLR Just-In-Time compiler
    * <b>clretwrc.dll</b>: CLR resources
    * <b>clrcompression.dll</b>: CLR Native data compression routines
    * <b>ngen.exe</b>: Native Image Generator
    * <b>MsBuild.exe</b>: Microsoft Build Engine
    * <b>mscordacwks.dll</b>: Multilanguage Standard Common Object Runtime data access
    * <b>mscordbi.dll</b>: Multilanguage Standard Common Object Runtime debugging services
    * <b>mscoreei.dll</b>: Multilanguage Standard Common Object Runtime Execution Engine Shim Implementation
    * <b>mscoreeis.dll</b>: Multilanguage Standard Common Object Runtime Execution Engine Shim Implementation
    * <b>mscorlib.dll</b>: Multilanguage Standard Common Object Runtime Class Library
    * <b>mscorpehost.dll</b>: Multilanguage Standard Common Object Runtime PE File Generator
    * <b>mscorrc.dll</b>: Multilanguage Standard Common Object Runtime ressources
    * <b>mscorsecimpl.dll</b>: Multilanguage Standard Common Object Runtime Security module
    * <b>mscorsn.dll</b>: Multilanguage Standard Common Object Runtime strong name support
    * <b>mscorsvc.dll</b>: Multilanguage Standard Common Object Runtime optimization service
    * <b>mscorsvw.exe</b>: Multilanguage Standard Common Object Runtime optimization service
    * <b>ilasm.exe</b>: IL Assembler
    * <b>ildasm.exe</b>: IL Disassembler
* Framework64


See: [All .NET Framework Tools](https://docs.microsoft.com/en-us/dotnet/framework/tools/)

<br />


#### 2. Microsoft SDK folder ####

`C:\Program Files (x86)\Microsoft SDKs\Windows`

There are different SDK versions: 

| SDK Version | Details                                                                                                                                 |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| v7.0        | Microsoft Windows SDK for Windows 7 and .NET Framework 3.5 SP1                                                                          |
| v7.0A       | Included in Visual Studio 2010. .NET Framework 4. Works only with Visual Studio 2010 and not Visual Studio 2010 Express.                |
| v7.1        | Microsoft Windows SDK for Windows 7 and .NET Framework 4                                                                                |
| v7.1A       | Included in Visual Studio 2012 Update 1 (or later)                                                                                      |
| v8.0        | Microsoft Windows SDK for Windows 8 and .NET Framework 4.5. .NET Framework 4.5, Windows Store apps and Integrated DirectX SDK           |
| v8.0A       | Included in Visual Studio 2012                                                                                                          |
| v8.1        | Windows Software Development Kit (SDK) for Windows 8.1 Windows 8.1, .NET Framework 4.5.1, Windows Store apps and Integrated DirectX SDK |
| v8.1A       | Included in Visual Studio 2013                                                                                                          |
| v10.0A      | Windows Standalone SDK for Windows 10. Included in Visual Studio 2015.                                                                  |


See: [All Windows SDK versions](https://en.wikipedia.org/wiki/Microsoft_Windows_SDK)


<br/>

Folder structure:

* v10.0A
  * bin
    * NETFX 4.6 Tools
    * NETFX 4.6 Tools
    * NETFX 4.7 Tools
    * NETFX 4.7.1 Tools
    * NETFX 4.7.2 Tools
      * <b>al.exe</b>: Assembly Linker
      * <b>aspnet_intern.exe</b>: Assembly interning
See more about: [Assembly Interning](https://www.shanebart.com/aspnet-assembly-interning/)
      * <b>aspnet_merge.exe</b>: ASP.NET Merge Tool
      * <b>AxImp.exe</b>: Windows Forms ActiveX Control Importer
      * <b>clrver.exe</b>: CLR version Tool
      * <b>CorFlags.exe</b>: CorFlags Conversion Tool
      * <b>disco.exe</b>: Web Services Discovery Tool 
      * <b>FUSLOGVW.exe</b>: Assembly Binding Log Viewer
      * <b>gacutil.exe</b>: Global Assembly Cache Tool
      * <b>ilasm.exe</b>: IL Assembler
      * <b>ildasm.exe</b>: IL Disassembler
      * <b>lc.exe</b>: License Compiler
      * <b>mage.exe</b>: Manifest Generation and Editing Tool
      * <b>mageui.exe</b>: Manifest Generation and Editing Tool, Graphical Client
      * <b>mgmtclassgen.exe</b>: Manifest Generation and Editing Tool, Graphical Client
      * <b>mpgo.exe</b>: Managed Profile Guided Optimization Tool
      * <b>MSBuildTaskHost.exe</b>: 
      * <b>PEVerify.exe</b>: PEVerify Tool
      * <b>ResGen.exe</b>: Resource File Generator
      * <b>SecAnnotate.exe</b>: .NET Security Annotator Tool
      * <b>sgen.exe</b>: XML Serializer Generator Tool
      * <b>sn.exe</b>: Strong Name Tool. Helps create assemblies with strong names. This tool provides options for key management, signature generation, and signature verification.
      * <b>SqlMetal.exe</b>: Generates code and mapping for the LINQ to SQL component of the .NET Framework.
      * <b>StoreAdm.exe</b>: Isolated Storage Tool. 
Manages isolated storage; provides options for listing the user's stores and deleting them.
      * <b>SvcConfigEditor.exe</b>: Configuration Editor Tool. The Windows Communication Foundation (WCF) Service Configuration Editor (SvcConfigEditor.exe) allows administrators and developers to create and modify configuration settings for WCF services using a graphical user interface. With this tool, you can manage settings for WCF bindings, behaviors, services, and diagnostics without having to directly edit XML configuration files.
      * <b>SvcTraceViewer.exe</b>: Service Trace Viewer Tool.Windows Communication Foundation (WCF) Service Trace Viewer Tool helps you analyze diagnostic traces that are generated by WCF. Service Trace Viewer provides a way to easily merge, view, and filter trace messages in the log so that you can diagnose, repair, and verify WCF service issues.
      * <b>SvcUtil.exe</b>: The ServiceModel Metadata Utility tool is used to generate service model code from metadata documents, and metadata documents from service model code.
      * <b>TlbExp.exe</b>: Type Library Exporter. It
generates a type library that describes the types that are defined in a common language runtime assembly.
      * <b>TlbImp.exe</b>: Type Library Importer. It
converts the type definitions found in a COM type library into equivalent definitions in a common language runtime assembly.
      * <b>Tracker.exe</b>
      * <b>WCA.exe</b>: Workflow Communication Activities Generation
      * <b>WFC.exe</b>
      * <b>WinMDExp.exe</b>: Windows Runtime Metadata Export Tool. It exports a .NET Framework assembly that is compiled as a .winmdobj file into a Windows Runtime component, which is packaged as a .winmd file that contains both Windows Runtime metadata and implementation information.
      * <b>WinRes.exe</b>: Windows Forms Resource Editor. It helps you localize user interface (UI) resources (.resx or .resources files) that are used by Windows Forms. You can translate strings, and then size, move, and hide controls to accommodate the localized strings.
      * <b>wsdl.exe</b>: Web Services Description Language. 
      * <b>xsd.exe</b>: The XML Schema Definition (Xsd.exe) tool generates XML schema or common language runtime classes from XDR, XML, and XSD files, or from classes in a runtime assembly. See more: [xsd](https://docs.microsoft.com/en-us/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe)
      * <b>xsltc.exe</b>: eXtensible Stylesheet Language Transformations. XSLT compiler compiles XSLT style sheets and generates an assembly. See more: [xsltc](https://docs.microsoft.com/en-us/dotnet/standard/data/xml/xslt-compiler-xsltc-exe)

<br />


#### 3. Visual Studio folder ####

`C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE`

Folder structure:

* Community
    * Common7
      * IDE
        * <b>Blend.exe</b>: WPF application designer
        * <b>DDConfigCA.exe</b>
        * <b>devenv.exe</b>: Visual Studio
        * <b>FeedbackCollector.exe</b>
        * <b>Microsoft.Visual Studio.Web.Host.exe</b>
        * <b>mspdbsrv.exe</b>: <b>M</b>icro<b>s</b>oft <b>P</b>rogram <b>D</b>ata<b>b</b>ase <b>S</b>e<b>rv</b>ice. Mspdbsrv.exe is a program used by Visual Studio to generate the symbols (PDB files). Requests related to creating, accessing or writing to PDB files are handled by mspdbsrv.exe.  
        * <b>MSTest.exe</b>: MSTest.exe is the command-line command that is used to run tests.
        * <b>PerfWatson2.exe</b>: 
        * <b>Publicize.exe</b>
        * <b>QTAgent.exe</b>: MsTest.exe call QTAgent.exe to run tests on agents.
        * <b>QTAgent_35.exe</b>
        * <b>QTAgent_40.exe</b>
        * <b>QTAgent32.exe</b>
        * <b>QTAgent32_35.exe</b>
        * <b>QTAgent32_40.exe</b>
        * <b>QTDCAgent.exe</b>
        * <b>QTDCAgent32.exe</b>
        * <b>StorePID.exe</b>
        * <b>T4VSHostProcess.exe</b>
        * <b>TCM.exe</b>
        * <b>TextTransform.exe</b>
        * <b>TfsLabConfig.exe</b>
        * <b>UserControlTestContainer.exe</b>
        * <b>vb7to8.exe</b>
        * <b>VsDebugWERHelper.exe</b>
        * <b>vsdiag_regwcf.exe</b>
        * <b>VSFinalizer.exe</b>
        * <b>VSHiveStub.exe</b>
        * <b>vshost.exe</b>: host process.  It is created whenever you build a project in the Visual Studio 2005 IDE. Its purpose is to provide support for improved F5 performance, partial trust debugging, and design time expression evaluation. See more: [vshost](https://blogs.msdn.microsoft.com/dtemp/2004/08/17/vshost-the-hosting-process/)
        * <b>vshost-clr2.exe</b>
        * <b>vshost32.exe</b>
        * <b>vshost32-clr2.exe</b>
        * <b>VSInitializer.exe</b>
        * <b>VSIXInstaller.exe</b>
        * <b>VSLaunchBrowser.exe</b>
        * <b>vsn.exe</b>
        * <b>VsRegEdit.exe</b>
        * <b>VSWebHandler.exe</b>
        * <b>VSWebLauncher.exe</b>
        * <b>WcfSvcHost.exe</b>: Windows Communication Foundation (WCF) Service Host (WcfSvcHost.exe) allows you to launch the Visual Studio debugger (F5) to automatically host and test a service you have implemented. You can then test the service using WCF Test Client (WcfTestClient.exe), or your own client, to find and fix any potential errors. See more: [WcfSvcHost.exe](https://docs.microsoft.com/en-us/dotnet/framework/wcf/wcf-service-host-wcfsvchost-exe)
        * <b>WcfTestClient.exe</b>: Windows Communication Foundation (WCF) Test Client (WcfTestClient.exe) is a GUI tool that enables users to input test parameters, submit that input to the service, and view the response that the service sends back. It provides a seamless service testing experience when combined with WCF Service Host. See more: [WcfTestClient.exe](https://docs.microsoft.com/en-us/dotnet/framework/wcf/wcf-test-client-wcftestclient-exe)
        * <b>XDesProc.exe</b>


#### 4. .NET Core SDK Folder ####


```cmd
C:\Users\xxx>dotnet --list-sdks
2.1.811 [C:\Program Files\dotnet\sdk]
3.1.404 [C:\Program Files\dotnet\sdk]
5.0.101 [C:\Program Files\dotnet\sdk]
```

