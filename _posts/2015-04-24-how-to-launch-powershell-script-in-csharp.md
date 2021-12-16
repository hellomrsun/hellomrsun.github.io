---
layout: post
read_time: true
show_date: true
title:  How to launch Powershell script in CSharp?
date:   2015-04-24 08:00:00 +0100
description:  How to launch Powershell script in CSharp? C# PS
img: posts/uncategorized/powershell.png
tags: [Powershell]
author: SUN Jiangong
mathjax: yes
redirect_from:
  - /2015/04/24/how-to-launch-powershell-script-csharp.html
---


If you want to launch a powershell script in CSharp application, you don't necessarily need to construct a cmd command line to launch the script. 

 
You could make your life easier with following example:


Variable "script" is the full path of the powershell script

Variable "parameters" is an instance of type of IDictionary, which contains a bunch of parameter key/values.

<!--more-->

```csharp
using (var powerShellInstance = PowerShell.Create())
{
    //Prepare powershell execution
    powerShellInstance.AddCommand(script);
    powerShellInstance.AddParameters(parameters);

    //Execute powershell command and get the results
    var results = powerShellInstance.Invoke();

    var errors = powerShellInstance.Streams.Error;
    var sb = new StringBuilder();

    if (errors.Count > 0)
    {
        foreach (var error in errors)
        {
            sb.Append(error);
        }
        errorResult = sb.ToString();
    }
    else
    {
        foreach (var result in results)
        {
            sb.AppendLine(result.ToString());
        }
        executionResult = sb.ToString();
    }

    return errors.Count == 0;
}
 ```

Update: 2015-07-01


I've encountered a problem in executing a powershell script in staging server. 

In fact, the application use an system account to execute the powershell script. 
But the account doesn't have enough right to run the script.


The exception is : **PSSecurityException**
Here is the error details:

```batch
Message: AuthorizationManager check failed.
InnerException stack trace:    
at System.Management.Automation.AuthorizationManager.ShouldRunInternal(CommandInfo commandInfo, CommandOrigin origin, PSHost host)
InnerException: A command that prompts the user failed because the host program or the command type does not support user interaction. The host was attempting to request confirmation with the following message: Run only scripts that you trust. While scripts from the internet can be useful, this script can potentially harm your computer. Do you want to run xxx.ps1?
```


I've searched a lot on the internet.
Reproduce the same error is so important!
Firstly I've reproduced it in an integration environment by removing the service account from "Administrators" group.
You could go to "Local Users and Groups", then "Groups", then "Administrators" group. Choose the service account and remove it from the group.


Then, i've found that the problem is related to execution policy on the server.
So I've tested with the execution policy.
You could use open powershell.exe on the server. 

Execute command : 

```powershell
Get-ExecutionPolicy
```

You could even verify the execution policy for a specific user.
You need to run powershell.exe by opening it with the service account.

Then execute command:

```powershell
Get-ExecutionPolicy -Scope:CurrentUser
```

In my server the execution policy was set to Unrestricted at LocalMachine scope.


There are 7 execution policies in all.
- Default: This equals to Restricted
- Restricted: Do not load configuration files or run scripts. This is the default.
- AllSigned: Require that all scripts and configuration files be signed by a trusted publisher, including scripts that you write on the local computer.
- RemoteSigned: Require that all scripts and configuration files downloaded from the Internet be signed by a trusted publisher.
- Unrestricted: Load all configuration files and run all scripts. If you run an unsigned script that was downloaded from the internet, you are prompted for permission before it runs.
- Bypass: Nothing is blocked and there are no warnings or prompts.
- Undefined: Remove the currently assigned execution policy from the current scope. This parameter will not remove an execution policy that is set in a Group Policy scope.


There are 5 scopes:
- Process
- CurrentUser
- LocalMachine
- UserPolicy
- MachinePolicy


Actually, it's the execution policy prevent the service account from running the script correctly.
So I need to modify the execution policy. Finally, ByPass meets my need.
But I would not apply this execution policy at local machine scope for all kinds of users.
So I applied the ByPass execution policy only to the service account.


The command used is:

```powershell
Set-ExecutionPolicy -Scope:CurrentUser -ExecutionPolicy:Bypass
```

I hope you find this article helpful!

<br/>

**References:**

https://blog.netspi.com/15-ways-to-bypass-the-powershell-execution-policy/

http://ss64.com/ps/powershell.html

http://blogs.msdn.com/b/kebab/archive/2014/04/28/executing-powershell-scripts-from-c.aspx

https://technet.microsoft.com/en-us/magazine/ff629472.aspx

http://virot.eu/is-your-execution-policy-unrestricted-for-the-entire-machine/
