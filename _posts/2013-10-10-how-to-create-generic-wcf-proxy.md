---
layout: post
title: How to create proxy to consume WCF service ?
description: How to create proxy to consume WCF service ?
excerpt_separator:  <!--more-->
tags: WCF
canonical_url: 'https://sunjiangong.com/create-proxy-to-consume-wcf-service/'
---

You want to consume a WCF service, but don't want to Add hard reference of the service's .svc file.

You can do it by this way.

You can add a hard reference of the WCF service's .svc file in a temporary project, and get its ServiceContract and DataContract classes.

If you have the source code of WCF service, you can get them directly from the source code.

<!--more-->

Then, paste the ServiceContract and DataContract classes in your client project.

```csharp        
        [ServiceContract]
        public interface IHelloWorldService
        {
            [OperationContract]
            string GetMessage(string name);
 
            [OperationContract]
            string GetPersonCompleteInfo(Person person);
        }
 
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
```

Create WCF channel directly with the WCF service address and service interface.

Then you can consume the service without any .svc file reference.

```csharp
        static void Main(string[] args)
        {
            WSHttpBinding basicHttpBinding = new WSHttpBinding();
            EndpointAddress endpointAddress = new EndpointAddress("http://localhost:8080/HostDevServer/HelloWorldService.svc");
            var service = new ChannelFactory<IHelloWorldService>(basicHttpBinding, endpointAddress).CreateChannel();
            var message = service.GetMessage("hello world!");
            Console.WriteLine(message);
        }
```





Enjoy coding! 