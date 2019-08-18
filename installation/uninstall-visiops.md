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



