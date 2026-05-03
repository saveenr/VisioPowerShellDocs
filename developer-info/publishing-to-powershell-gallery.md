# Publis to PowerShell Gallery

The Visio PowerShell module is distributed via the PowerShell gallery: [https://www.powershellgallery.com/packages/Visio/](https://www.powershellgallery.com/packages/Visio/)

Instructions to publish&#x20;

### PREREQ

You must be package owner of Visio

### STEP 1 Get an API Key

Login to: [https://www.powershellgallery.com/account/apikeys](https://www.powershellgallery.com/account/apikeys)

You either have it already, or you need to regenerate it.

### STEP 2 Install module locally

First install the module for the Current User.

This means the module must be in this location:

`$home\Documents\WindowsPowerShell\Modules`

Which maps to something like `C:\Users\username\Documents\WindowsPowerShell\Modules`



You can use the InstallForCurrentUser.ps1 script in the VisioPowerShell folder

### STEP 3 Publish

Then use publish-module

```
$key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
Publish-Module -Name "Visio" -NuGetApiKey $key
```
