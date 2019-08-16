# Install VisioPS

You can find VisioPS in [**the PowerShell Gallery**](https://www.powershellgallery.com/packages/Visio/).

**To install for all users** \(needs Administrator rights\)

```text
Install-Module Visio
```

**To install for current user** \(does not need Administrator rights\)

```text
Install-Module Visio -Scope CurrentUser
```

The `Install-Module` cmdlet comes with PowerShell 5.0 which is part of with Microsoft Windows 10. To get PowerShell 5.0 for earlier versions of Microsoft Windows see the instructions here: [Windows Management Framework 5.0 or above](https://docs.microsoft.com/en-us/powershell/wmf/readme)

