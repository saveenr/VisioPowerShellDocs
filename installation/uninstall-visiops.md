# Uninstall VisioPS

### Before uninstalling

Close all instances of **PowerShell** and **PowerShell ISE** and any other PowerShell clients

### **Uninstall method 1**

```text
Get-Module -ListAvailable -Name Visio  | Uninstall-Module
```

### **Uninstall method 2**

First find the module's location

```text
Get-Module -ListAvailable -Name Visio
```

Then delete the `Visio` folder.

### **Verify VisioPS is not installed**

Use the `Get-Module` cmdlet to verify that it is gone. For example:

```text
$modules = Get-Module -Name "Visio"
if ($modules -eq $null)
{
    Write-Host "VisioPS" not installed
}
else
{
    Write-Host "VisioPS" is installed
}
```



