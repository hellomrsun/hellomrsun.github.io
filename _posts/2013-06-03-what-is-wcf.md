---
layout: post
read_time: true
show_date: true
title:  What is WCF?
date:   2013-06-03 08:00:00 +0100
description: What is WCF? Windows Communication Framework
img: posts/uncategorized/wcf.PNG
tags: [WCF]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/what-is-wcf.html'
---


### What is WCF and how it works?

Windows Communication Foundation is a framework for intercommunication between different applications regardless of their languages.

<!--more-->

Example:

IHelloWorldService.cs:

```csharp
using System.Runtime.Serialization; //used for DataContract.
using System.ServiceModel; //used for ServiceContract. 
//it contains the types necessary to build Windows Communication Foundation (WCF) service and client applications.
 
namespace MyWCFServices
{
    [ServiceContract]
    public interface IHelloWorldService
    {
        [OperationContract]
        string GetMessage(string name);
 
        [OperationContract]
        string GetPersonCompleteInfo(Person person);
    }
 
    //DataContract is used to be transmitted between web service and client
    [DataContract]
    public class Person
    {
        [DataMember]
        public int Age { get; set; }
 
        [DataMember]
        public string Sex { get; set; }
 
        [DataMember]
        public string Name { get; set; }
    }
}
```

HelloWorldService.cs:
```csharp
/// <summary>
/// Create a service class and implement service interface
/// </summary>
public class HelloWorldService : IHelloWorldService
{
    public string GetMessage(string name)
    {
        return "Hello world from " + name + "!";
    }

    public string GetPersonCompleteInfo(Person compInfo)
    {
        return "Person complete info( age is:" + compInfo.Age + ";sex is:" + compInfo.Sex + ";name is:" + compInfo.Name + ")";
    }
}
```

<br />

### WCF vs ASMX web service:

AXMX web service is just add WebMethod attribute to methods.

Example:

```csharp
[WebMethod]
public string MyMethod(string text)
{     
return "Hello" + text;
}
```

WCF use interface , the class implements interface which provide encapsulation and security.

<br />

### WCF binding types:

BasicHttpBinding is designed to replace ASMX Web services. It supports both HTTP and Secure HTTP. As far as encoding is concerned, it provides support for Text as well as MTOM encoding methods. BasicHttpBinding doesn’t support WS-* standards like WS-Addressing, WS-Security and WS-ReliableMessaging.

WsHttpBinding also supports interoperability. With this binding, the SOAP message is, by default, encrypted. It supports HTTP and HTTPS. In terms of encoding, it provides support for Text as well as MTOM encoding methods. It supports WS-* standards like WS-Addressing, WS-Security and WS-ReliableMessaging. By default, reliable sessions are disabled because it can cause a bit of performance overhead.

<br />

### EndPoint                                                                            

```csharp
<endpoint address="http://localhost:8080/HostDevServer/HelloWorldService.svc"
            binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_IHelloWorldService"
            contract="HelloWorldService.IHelloWorldService" name="WSHttpBinding_IHelloWorldService">
            <identity>
                <userPrincipalName value="username" />
            </identity>
</endpoint>
```

**ABC**: Address, Binding, Contract

<br />

### WCF vs REST


WCF Service is Microsoft's implementation of SOAP. There are others implementations or you could roll your own (not recommended).

SOAP is a kind of stateful, session-based, message-based web service. It's good if your service is designed as a set of complex actions.

REST is a stateless, sessionless, resource-based web service. It's good if your service is designed to access data and perform simple CRUD operations on it. SOAP and REST are mutually exclusive. A service cannot be both. There are ways to manipulate vanilla WCF to make is RESTful but these techniques are becoming deprecated. If you want to implement a RESTful web service there are two main choices in the Microsoft world: WCF Data Services and ASP.NET Web API.

WCF binding: basicHttpBinding, wsHttpBinding

REST binding: webHttpBinding, mexHttpBinding