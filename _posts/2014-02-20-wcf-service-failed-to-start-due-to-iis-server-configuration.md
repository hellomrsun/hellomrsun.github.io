---
layout: post
read_time: true
show_date: true
title:  WCF service failed to start due to IIS server configuration
date:   2014-02-20 08:00:00 +0100
description: WCF service failed to start due to IIS server configuration
img: posts/uncategorized/iis.png
tags: [IIS, WCF]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/wcf-service-failed-to-start-due-to-iis-server-configuration.html'
---


I've encountered a problem when I deploy a web service in a new environment. While I've used the same binary work correctly in another server.


Here is a error message:

```batch
System.ServiceModel.ServiceActivationException: The service cannot be activated due to an exception during compilation. 
```

<!--more-->

The exception message is: 

```batch
The authentication schemes configured on the host ('IntegratedWindowsAuthentication') do not allow those configured on the binding 'WSHttpBinding' ('Anonymous'). Please ensure that the SecurityMode is set to Transport or TransportCredentialOnly.
```

Additionally, this may be resolved by changing the authentication schemes for this application through the IIS management tool, through the ServiceHost.Authentication.AuthenticationSchemes property, in the application configuration file at the <serviceAuthenticationManager> element, by updating the ClientCredentialType property on the binding, or by adjusting the AuthenticationScheme property on the HttpTransportBindingElement.

Then I had this error:

```batch
System.NotSupportedException: The authentication schemes configured on the host ('IntegratedWindowsAuthentication') do not allow those configured on the binding 'WSHttpBinding' ('Anonymous'). 
```

So I've found that it shouldn't be a problem of my code, while it's a problem of IIS configuration.


To check the configuration, you need to go to -> %systemroot%\System32\inetsrv\config

You can compare all the configurations between this server and another server where the service works in.

For me, it was a configuration problem in applicationHost.config. And I just need to activate the anonymous anthentication.

```batch
<location path="DEV.MARKET.Global">
        <system.webServer>
            <security>
                <authentication>
                    <anonymousAuthentication enabled="true" />
                    <windowsAuthentication enabled="true" authPersistNonNTLM="true" />
                </authentication>
            </security>
        </system.webServer>
    </location>
```

So the probme is solved!

Hoping this post can help others! :)
