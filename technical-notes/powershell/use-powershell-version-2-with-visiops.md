# Use PowerShell 2 with .NET Framework 2.0

PowerShell 2 uses .NET Framework's 2.0 by default. 

If you use PowerShell 2 and try to import the a module \(such as VisioPS\) which requires .NET Framework 4.0, you'll get an error like this:

```text
This assembly is built by a runtime newer than the currently loaded 
runtime and cannot be loaded.”
```

To see what versions any version of Powershell is using, look at `$PSVersionTable`**.** For example, below is an example of `$PSVersionTable` from a Windows 7 machine running Powershell. The `CLRVersion` indicates which version of the .NET Framework is used and in this case it begins with "2". 

```text
Name Value
--- ---
PSVersion 2.0
PSEdition Desktop
PSCompatibleVersions {1.0, 2.0}                         
BuildVersion 6.1.7601.17514
PSRemotingProtocolVersion 2.1
WSManStackVersion 2.0
CLRVersion 2.0.50727.6456
SerializationVersion 1.1.0.1
```

VisioPS requires a .NET Framework 4.0. 

Notice the value or **CLRVersion** begins with a "2".

In any case, this is a common occurrence with a straightforward solution. You can force PowerShell to start using the .NET Framework 4.0 [as documented in this StackOverflow question](http://stackoverflow.com/questions/2094694/how-can-i-run-powershell-with-the-net-4-runtime). The procedure involves creating two small XML files and placing them in the appropriate place.

Here is a small PowerShell script that will automatically create and place the necessary files. **Be aware that the script as shown below will overwrite existing .config files**.

> $config\_text = @"  
> &lt;?xml version="1.0"?&gt;   
> &lt;configuration&gt;   
>     &lt;startup useLegacyV2RuntimeActivationPolicy="true"&gt;   
>         &lt;supportedRuntime version="v4.0.30319"/&gt;   
>         &lt;supportedRuntime version="v2.0.50727"/&gt;   
>     &lt;/startup&gt;   
> &lt;/configuration&gt;  
> "@
>
> $config\_text\| Out-File $pshome\powershell.exe.config  
> $config\_text\| Out-File $pshome\powershell\_ise.exe.config

Start **PowerShell as an Administrator** an then run the script. Then restart PowerShell and examine the value of `$PSVersionTable`**.** The value or `CLRVersion` ****now begins with a "4". Now your can load VisioPS or any other .NET 4.0 module correctly.

```text
Name Value
--- ---
PSVersion 2.0
PSEdition Desktop
PSCompatibleVersions {1.0, 2.0}                         
BuildVersion 6.1.7601.17514
PSRemotingProtocolVersion 2.1
WSManStackVersion 2.0
CLRVersion 4.0.30319.42000
SerializationVersion 1.1.0.1
```

