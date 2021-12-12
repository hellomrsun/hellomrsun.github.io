---
layout: post
# title: What is the difference between ASMX, WCF, and ASP.NET Web API?
# excerpt_separator:  <!--more-->
# tags: DotNet | Web-Service | Web-Api
# canonical_url: 'https://sunjiangong.com/what-is-the-difference-between-asmx-wcf-and-asp-net-web-api/'
read_time: true
show_date: true
title:  What is the difference between ASMX, WCF, and ASP.NET Web API?
date:   2020-02-16 08:00:00 +0100
description: What is the difference between ASMX, WCF, and ASP.NET Web API? Windows communication framework
img: posts/2020-02-16-AsmxWcfWebApi/asmx-wcf-webapi.png
tags: [DotNet, WebService, WebApi, WCF]
author: SUN Jiangong
# github:  hellomrsun
mathjax: yes
---

Application architecture has evolved from monolithic architecture to SOA architecture in order to make better separation, then to more refined microservice architecture today.

Applications need to communicate among themselves, and to achieve this purpose, Microsoft has developed technologies like ASMX, WCF, and ASP.NET Web API.

Let's explore them together today.

<!--more-->

<!-- TOC -->

- [ASMX](#asmx)
  - [SOAP message](#soap-message)
  - [ASMX web service code sample](#asmx-web-service-code-sample)
  - [WSDL](#wsdl)
    - [WSDL structure](#wsdl-structure)
    - [PrintService's WSDL detail](#printservices-wsdl-detail)
    - [PrintService's WSDL code](#printservices-wsdl-code)
    - [SOAP vs WSDL vs UDDI](#soap-vs-wsdl-vs-uddi)
  - [ASMX service consumption](#asmx-service-consumption)
    - [Consume ASMX service in Web browser](#consume-asmx-service-in-web-browser)
    - [Consume ASMX service in SoapUI](#consume-asmx-service-in-soapui)
  - [ASMX project source project](#asmx-project-source-project)
- [WCF](#wcf)
  - [WCF Architecture](#wcf-architecture)
  - [WCF communication binding](#wcf-communication-binding)
  - [SOAP WCF service sample code](#soap-wcf-service-sample-code)
  - [SOAP WCF WSDL](#soap-wcf-wsdl)
    - [SOAP WCF WSDL detail](#soap-wcf-wsdl-detail)
    - [SOAP WCF WSDL code](#soap-wcf-wsdl-code)
  - [SOAP WCF service consumption](#soap-wcf-service-consumption)
  - [WCF service bindings](#wcf-service-bindings)
  - [REST WCF service sample code](#rest-wcf-service-sample-code)
  - [REST WCF WADL](#rest-wcf-wadl)
    - [REST WCF WADL structure](#rest-wcf-wadl-structure)
    - [REST WCF WADL code](#rest-wcf-wadl-code)
  - [REST WCF service consumption](#rest-wcf-service-consumption)
  - [SOAP and REST WCF services source projects](#soap-and-rest-wcf-services-source-projects)
- [ASP.NET Web API](#aspnet-web-api)
  - [REST](#rest)
  - [Web API sample code](#web-api-sample-code)
  - [Web API consumption](#web-api-consumption)
  - [Web API source project](#web-api-source-project)

<!-- /TOC -->

<br/>

# ASMX

<br/>

**ASMX** (ASP.NET Web Services) is the primary web service technology in .NET 1.0 and .NET 2.0.

ASMX provides the ability to build web services that send **SOAP** (Simple Object Access Protocol) messages over **HTTP** protocol.

## SOAP message

SOAP message is in **XML** format.

SOAP message request sample:

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tem="http://tempuri.org/">
    <soapenv:Header />
    <soapenv:Body>
        <tem:GetFullName>
            <!--Optional:-->
            <tem:firstName>jiangong</tem:firstName>
            <!--Optional:-->
            <tem:lastName>sun</tem:lastName>
        </tem:GetFullName>
    </soapenv:Body>
</soapenv:Envelope>
```

## ASMX web service code sample

```csharp
using System.Web.Services;
namespace AsmxWebService
{
    [WebService(Namespace = "http://tempuri.org/")]
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
    [System.ComponentModel.ToolboxItem(false)]
    public class NameService : System.Web.Services.WebService
    {
        [WebMethod]
        public string GetFullName(string firstName, string lastName)
        {
            return $"{firstName} {lastName}";
        }
    }
}
```

<br/>


## WSDL

**WSDL** (Web Service Description Language) is a language to describe the service.

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Asmx_soapui_wsdl.PNG)

<br/>

### WSDL structure

| **WSDL Section** | **Description**                                                              |
| ------------ | ------------------------------------------------------------------------ |
| types        | Defines the (XML Schema) data types used by the web service              |
| message      | Defines the data elements for each operation                             |
| portType     | Describes the operations that can be performed and the messages involved |
| binding      | Defines the protocol and data format for each port type                  |

<br/>

### PrintService's WSDL detail

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Asmx_soapui_wsdl_structure.PNG)

### PrintService's WSDL code

```xml
<wsdl:definitions targetNamespace="http://tempuri.org/" xmlns:tm="http://microsoft.com/wsdl/mime/textMatching/" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/" xmlns:mime="http://schemas.xmlsoap.org/wsdl/mime/" xmlns:tns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/" xmlns:s="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://schemas.xmlsoap.org/wsdl/soap12/" xmlns:http="http://schemas.xmlsoap.org/wsdl/http/" xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/">
   <wsdl:types>
      <s:schema elementFormDefault="qualified" targetNamespace="http://tempuri.org/">
         <s:element name="GetFullName">
            <s:complexType>
               <s:sequence>
                  <s:element minOccurs="0" maxOccurs="1" name="firstName" type="s:string"/>
                  <s:element minOccurs="0" maxOccurs="1" name="lastName" type="s:string"/>
               </s:sequence>
            </s:complexType>
         </s:element>
         <s:element name="GetFullNameResponse">
            <s:complexType>
               <s:sequence>
                  <s:element minOccurs="0" maxOccurs="1" name="GetFullNameResult" type="s:string"/>
               </s:sequence>
            </s:complexType>
         </s:element>
      </s:schema>
   </wsdl:types>
   <wsdl:message name="GetFullNameSoapIn">
      <wsdl:part name="parameters" element="tns:GetFullName"/>
   </wsdl:message>
   <wsdl:message name="GetFullNameSoapOut">
      <wsdl:part name="parameters" element="tns:GetFullNameResponse"/>
   </wsdl:message>
   <wsdl:portType name="NameServiceSoap">
      <wsdl:operation name="GetFullName">
         <wsdl:input message="tns:GetFullNameSoapIn"/>
         <wsdl:output message="tns:GetFullNameSoapOut"/>
      </wsdl:operation>
   </wsdl:portType>
   <wsdl:binding name="NameServiceSoap" type="tns:NameServiceSoap">
      <soap:binding transport="http://schemas.xmlsoap.org/soap/http"/>
      <wsdl:operation name="GetFullName">
         <soap:operation soapAction="http://tempuri.org/GetFullName" style="document"/>
         <wsdl:input>
            <soap:body use="literal"/>
         </wsdl:input>
         <wsdl:output>
            <soap:body use="literal"/>
         </wsdl:output>
      </wsdl:operation>
   </wsdl:binding>
   <wsdl:binding name="NameServiceSoap12" type="tns:NameServiceSoap">
      <soap12:binding transport="http://schemas.xmlsoap.org/soap/http"/>
      <wsdl:operation name="GetFullName">
         <soap12:operation soapAction="http://tempuri.org/GetFullName" style="document"/>
         <wsdl:input>
            <soap12:body use="literal"/>
         </wsdl:input>
         <wsdl:output>
            <soap12:body use="literal"/>
         </wsdl:output>
      </wsdl:operation>
   </wsdl:binding>
   <wsdl:service name="NameService">
      <wsdl:port name="NameServiceSoap" binding="tns:NameServiceSoap">
         <soap:address location="http://localhost:61331/PrintService.asmx"/>
      </wsdl:port>
      <wsdl:port name="NameServiceSoap12" binding="tns:NameServiceSoap12">
         <soap12:address location="http://localhost:61331/PrintService.asmx"/>
      </wsdl:port>
   </wsdl:service>
</wsdl:definitions>
```

See more information about WSDL: [W3C WSDL Specification](https://www.w3.org/TR/wsdl20/)

<br/>

### SOAP vs WSDL vs UDDI

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_wsdl_soap_uddi.gif)

<br/>

## ASMX service consumption

To consume the ASMX service, you can use any web browser or SoapUI.

### Consume ASMX service in Web browser

**Call:**

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Asmx_browser_call.PNG)

**Result:**

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Asmx_browser_response.PNG)

### Consume ASMX service in SoapUI

To consume the WCF service in SoapUI, you must enter a .WSDL suffix after .asmx.

Call and result:

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Asmx_soapui_call.PNG)

<br/>

## ASMX project source project

Download [SOAP ASMX service sample project](https://github.com/hellomrsun/BlogCodeSource/tree/master/src/2020-02-16_ASMX_WCF_WebApi/01_ASMX/AsmxWebService)

<br/><br/>

# WCF

<br/>

**WCF** (Windows Communication Foundation) is a framework for building service-oriented applications.
WCF  is introduced since .NET 3.0.

## WCF Architecture

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_architecture.gif)
Source: Microsoft

<br/>

## WCF communication binding
![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_binding.gif)
Source: Microsoft

<br/>

## SOAP WCF service sample code

WCF can transfer **SOAP** messages over **HTTP** protocol by default, just like **ASMX** service.

SOAP WCF service sample code.

```csharp
[ServiceContract]
public interface IPrintService
{
    [OperationContract]
    Name GetFullName(string firstName, string lastName);
}

public class PrintService : IPrintService
{
    public Name GetFullName(string firstName, string lastName)
    {
        return new Name
        {
            FirstName = firstName,
            LastName = lastName
        };
    }
}
```

<br/>


## SOAP WCF WSDL

**SOAP WCF WSDL**
![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_soap_soapui_wsdl.PNG)

<br/>

### SOAP WCF WSDL detail
![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_soap_soapui_wsdl_structure.PNG)

<br/>

### SOAP WCF WSDL code

```xml
<wsdl:definitions name="PrintService" targetNamespace="http://tempuri.org/" xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/" xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd" xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/" xmlns:soap12="http://schemas.xmlsoap.org/wsdl/soap12/" xmlns:tns="http://tempuri.org/" xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing" xmlns:wsx="http://schemas.xmlsoap.org/ws/2004/09/mex" xmlns:wsap="http://schemas.xmlsoap.org/ws/2004/08/addressing/policy" xmlns:wsaw="http://www.w3.org/2006/05/addressing/wsdl" xmlns:msc="http://schemas.microsoft.com/ws/2005/12/wsdl/contract" xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy" xmlns:wsa10="http://www.w3.org/2005/08/addressing" xmlns:wsam="http://www.w3.org/2007/05/addressing/metadata">
   <wsdl:types>
      <xsd:schema targetNamespace="http://tempuri.org/Imports">
         <xsd:import schemaLocation="http://localhost:61543/PrintService.svc?xsd=xsd0" namespace="http://tempuri.org/"/>
         <xsd:import schemaLocation="http://localhost:61543/PrintService.svc?xsd=xsd1" namespace="http://schemas.microsoft.com/2003/10/Serialization/"/>
         <xsd:import schemaLocation="http://localhost:61543/PrintService.svc?xsd=xsd2" namespace="http://schemas.datacontract.org/2004/07/WcfSoapWebService"/>
      </xsd:schema>
   </wsdl:types>
   <wsdl:message name="IPrintService_GetFullName_InputMessage">
      <wsdl:part name="parameters" element="tns:GetFullName"/>
   </wsdl:message>
   <wsdl:message name="IPrintService_GetFullName_OutputMessage">
      <wsdl:part name="parameters" element="tns:GetFullNameResponse"/>
   </wsdl:message>
   <wsdl:portType name="IPrintService">
      <wsdl:operation name="GetFullName">
         <wsdl:input wsaw:Action="http://tempuri.org/IPrintService/GetFullName" message="tns:IPrintService_GetFullName_InputMessage"/>
         <wsdl:output wsaw:Action="http://tempuri.org/IPrintService/GetFullNameResponse" message="tns:IPrintService_GetFullName_OutputMessage"/>
      </wsdl:operation>
   </wsdl:portType>
   <wsdl:binding name="BasicHttpBinding_IPrintService" type="tns:IPrintService">
      <soap:binding transport="http://schemas.xmlsoap.org/soap/http"/>
      <wsdl:operation name="GetFullName">
         <soap:operation soapAction="http://tempuri.org/IPrintService/GetFullName" style="document"/>
         <wsdl:input>
            <soap:body use="literal"/>
         </wsdl:input>
         <wsdl:output>
            <soap:body use="literal"/>
         </wsdl:output>
      </wsdl:operation>
   </wsdl:binding>
   <wsdl:service name="PrintService">
      <wsdl:port name="BasicHttpBinding_IPrintService" binding="tns:BasicHttpBinding_IPrintService">
         <soap:address location="http://localhost:61543/PrintService.svc"/>
      </wsdl:port>
   </wsdl:service>
</wsdl:definitions>
```

<br/>

## SOAP WCF service consumption

**Add WSDL in SoapUI:**

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_soap_wsdl.PNG)

PrintService.svc's **.svc** means Service.

**SOAP WCF service consumption:**

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_soap_soapui_call.PNG)

<br/>

## WCF service bindings

In addition, WCF provides much more features to build secure, complex WCF services.
WCF can work with other protocols like **TCP**, **HTTPS**, and **UDP**.

<br/>

Here are all the WCF Bindings:

| Binding type | Note | Description |
| ------------ | ---- | ----------- ||
| BasicHttpBinding            | it's the **most used** binding | A binding that is suitable for communicating with WS-Basic Profile conformant Web services, for example, ASP.NET Web services (ASMX)-based services. This binding uses HTTP as the transport and text/XML as the default message encoding. |
| WSHttpBinding               | secure **HTTPS** binding    | A secure and interoperable binding that is suitable for non-duplex service contracts.                                                                                                                                                      |
| WS2007HttpBinding           |                       | A secure and interoperable binding that provides support for the correct versions of the Security, ReliableSession, and TransactionFlow binding elements.                                                                                  |
| WSDualHttpBinding           |                       | A secure and interoperable binding that is suitable for duplex service contracts or communication through SOAP intermediaries.                                                                                                             |
| WSFederationHttpBinding     |                       | A secure and interoperable binding that supports the WS-Federation protocol, enabling organizations that are in a federation to efficiently authenticate and authorize users.                                                              |
| WS2007FederationHttpBinding |                       |
| NetTcpBinding               |     it uses **TCP** protocol to transfer messages, and **faster** than WSHttpBinding                  | A secure and optimized binding suitable for cross-machine communication between WCF applications.                                                                                                                                          |
| NetNamedPipeBinding         |                       | A secure, reliable, optimized binding that is suitable for on-machine communication between WCF applications.                                                                                                                              |
| NetMsmqBinding              |   it can work with **MSMQ** (Message Queuing)                   | A queued binding that is suitable for cross-machine communication between WCF applications.                                                                                                                                                |
| NetPeerTcpBinding           |                       | A binding that enables secure, multi-machine communication.                                                                                                                                                                                |
| WebHttpBinding              |  **RESTful** service, passing **HTTP** message instead of SOAP message over HTTP protocol                     | A binding used to configure endpoints for WCF Web services that are exposed through HTTP requests instead of SOAP messages.                                                                                                                |
| MsmqIntegrationBinding      |                       | A binding that is suitable for cross-machine communication between a WCF application and existing Message Queuing (also known as MSMQ) applications.                                                                                       |
|NetHttpBinding| **WebSocket** communication, introduced in .NET 4.5 | NetHttpBinding is a binding designed for consuming HTTP or WebSocket services and uses binary encoding by default.  |
|NetHttpsBinding| **WebSocket** communication, introduced in .NET 4.5 | NetHttpsBinding is a secure binding designed for consuming HTTP or WebSocket services and uses binary encoding by default.|
|BasicHttpContextBinding| Derives from BasicHttpBinding | A binding suitable for communicating with WS-Basic Profile conformant Web services that enables HTTP cookies to be used to exchange context. |
|NetTcpContextBinding| Derives from NetTcpBinding | A secure and optimized binding suitable for cross-machine communication between WCF applications that enables SOAP headers to be used to exchange context. |
| WSHttpContextBinding | Derives from WsHttpBinding | A secure and interoperable binding suitable for non-duplex service contracts that enables SOAP headers to be used to exchange context. |
| UdpBinding | **UDP** | A binding to use when sending a burst of simple messages to a large number of clients simultaneously. |

<br/>

## REST WCF service sample code

WCF also can act as **RESTful** service with WebHttpBinding.

REST WCF service sample:

```csharp
[ServiceContract]
public interface IRestPrintService
{
    [OperationContract]
    [WebGet(UriTemplate = "/GetFullName", ResponseFormat = WebMessageFormat.Json)]
    string GetFullName();

    [OperationContract]
    [WebInvoke(UriTemplate = "/PostName/{firstName}/{lastName}", Method = "POST")]
    string PostNameInfo(string firstName, string lastName);
}

public class RestPrintService : IRestPrintService
{
    public string GetFullName()
    {
        return "{'name':'SUN Jiangong'}";
    }

    public string PostNameInfo(string firstName, string lastName)
    {
        var name = new Name
        {
            FirstName = firstName,
            LastName = lastName
        };

        return JsonConvert.SerializeObject(name);
    }
}
```

<br/>

## REST WCF WADL

**WADL** (Web Application Description Language) is a machine-readable XML description of HTTP-based web services.

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_rest_wadl.PNG)

<br/>

### REST WCF WADL structure

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_rest_wadl_structure.PNG)

<br/>

### REST WCF WADL code

```xml
<application xmlns="http://wadl.dev.java.net/2009/02">
   <doc xml:lang="en" title="http://localhost:61686"/>
   <resources base="http://localhost:61686">
      <resource path="RestPrintService.svc/PostName" id="PrintService.svc">
         <doc xml:lang="en" title="PrintService.svc"/>
         <method name="POST" id="PrintService.svc 1">
            <doc xml:lang="en" title="PrintService.svc 1"/>
            <request>
               <representation mediaType="application/json"/>
            </request>
            <response status="">
               <representation mediaType="application/json"/>
            </response>
            <response status="404">
               <representation mediaType="text/html; charset=UTF-8" element="html"/>
            </response>
            <response status="400">
               <representation mediaType="text/html" element="html"/>
            </response>
            <response status="200">
               <representation mediaType="application/xml; charset=utf-8" element="ser:string" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/"/>
            </response>
            <response status="0">
               <representation mediaType="" element="data"/>
            </response>
         </method>
      </resource>
   </resources>
</application>
```

<br/>

## REST WCF service consumption

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Wcf_rest_soapui_call.PNG)

<br/>

## SOAP and REST WCF services source projects

Download [SOAP and REST WCF service sample project](https://github.com/hellomrsun/BlogCodeSource/tree/master/src/2020-02-16_ASMX_WCF_WebApi/02_WCF/WcfWebService)

<br/>

# ASP.NET Web API

ASP.NET Web API pass messages over HTTP or HTTPS protocol.

Modern ASP.NET Web APIs are RESTful.

## REST

**REST** (RepreSentational State Transfer)

REST Web API has the following characteristics:

* Client-server architecture

The principle behind the client-server constraints is the separation of concerns.

* Statelessness

The client-server communication is constrained by no client context being stored on the server between requests. Each request from any client contains all the information necessary to service the request, and the session state is held in the client. The session state can be transferred by the server to another service such as a database to maintain a persistent state for a period and allow authentication.

* Cacheability

Well-managed caching partially or completely eliminates some client-server interactions, further improving scalability and performance.

* Layered system

* Code on demand (optional)

Servers can temporarily extend or customize the functionality of a client by transferring executable code

* Uniform interface

The uniform interface constraint is fundamental to the design of any RESTful system.

The four constraints for this uniform interface are:

* Resource identification in requests
* Resource manipulation through representations
* Self-descriptive messages
* Hypermedia as the engine of application state (HATEOAS)

<br/>

## Web API sample code

```csharp
[HttpGet]
[Route("api/v1/Values/{id}")]
public HttpResponseMessage Get(int id)
{
    var content = "{ 'id';" + id + "}";
    HttpResponseMessage response = Request.CreateResponse(HttpStatusCode.OK, "value");
    response.Content = new StringContent(content, Encoding.UTF8);
    return response;
}
```

<br/>

## Web API consumption

![](./../../../assets/img/posts/2020-02-16-AsmxWcfWebApi/Api_browser_call.PNG)

<br/>

## Web API source project

Download [ASP.NET Web API sample project](https://github.com/hellomrsun/BlogCodeSource/tree/master/src/2020-02-16_ASMX_WCF_WebApi/03_WebApi/AspNetWebApi)
