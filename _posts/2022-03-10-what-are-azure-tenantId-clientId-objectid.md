---
layout: post
read_time: true
show_date: true
title:  What are Azure TenantId, ClientId (Application Id) and ObjectId?
date:   2022-03-10 08:00:00 +0100
description: Azure Tenant Id, Client Id (Application Id), Object Id
img: posts/uncategorized/azure.png
tags: [Azure]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/what-are-aszure-tenant-id-client-id-object-id.html'
---

There are some Identifiers you have to know when you are using Azure.

They are: 
- Tenant Id
- Client Id (Application Id)
- Object Id

<!--more-->
<br>

### Tenant ID 

Tenant Id is the Azure Active Directory's Global unique identifier (GUID).

You can access it through the path: *Azure Portal > Azure Active Directory*

![](./../../../assets/img/posts/2022-03-10-azure-tenantid-clientid/azure-tenantid.png)

An example:

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "msidentitysamplestesting.onmicrosoft.com",
    "TenantId": "7f58f645-c190-4ce5-9de4-e2b7acd2a6ab",
    "ClientId": "a4c2469b-cf84-4145-8f5f-cb7bacf814bc"
  },
}
```

<br>

### Client ID (Equals to Application ID)

This is the unique application ID of this application in your directory. You can use this application ID if you ever need help from Microsoft Support, or if you want to perform operations against this specific instance of the application using the Azure Active Directory Graph or PowerShell APIs.

<br>
You can find the applications registered in your Azure subscription by *Azure AD => Enterprise applications => Application Name*.

![](./../../../assets/img/posts/2022-03-10-azure-tenantid-clientid/azure-applicationId.png)

<br>
You can log in the Azure with ClientId and ClientSecret and use it to manage user rights, or send emails etc.

Install the following Nuget packages to be able to authenticate in Graph API as an application.
- Microsoft.Identity.Client
- Microsoft.Graph
- Microsoft.Graph.Auth

<br>
Then you can create a graph service client to be able to manipulate a lot of things in Microsoft Graph API.
```csharp
var authorityUri = $"https://login.microsoftonline.com/{_tenantId}/v2.0";
var confidentialClientApplication = ConfidentialClientApplicationBuilder
    .Create(_clientId)
    .WithClientSecret(_clientSecret)
    .WithAuthority(new Uri(authorityUri))
    .Build();

var authProvider = new ClientCredentialProvider(confidentialClientApplication);
var graphserviceClient = new GraphServiceClient(authProvider);
```                

<br>

### Object Id

This is the unique ID of the service principal object associated with this application. This ID can be useful when performing management operations against this application using PowerShell or other programmatic interfaces.

As you can see in the previous chapter, Application has an "Application ID" and an "Object ID".

And an user also has an Object ID.

![](./../../../assets/img/posts/2022-03-10-azure-tenantid-clientid/azure-objectId.png)

You can use object IDs to retrieve all the roles assigned to an user in an application.

```csharp
public async Task<IUserAppRoleAssignmentsCollectionPage> GetUserRolesAsync(string userObjectId, 
                                                                          string applicationObjectId)
{
  return await graphserviceClient.Users[userObjectId].AppRoleAssignments.Request()
                                 .Filter($"resourceId eq {applicationObjectId}").GetAsync();
}
```

Now you have an idea about the different identifiers in Azure. 
