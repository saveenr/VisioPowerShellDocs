# Detect if VisioPS is installed

#### Detect if Visio PowerShell is installed <a id="detect-if-visio-powershell-is-installed"></a>

```text
Get-Module -ListAvailable -Name Visio  | Select Path
```

If it is installed it will show you exactly where. In the example below you can see it is installed for a specific user.

```text
Path
----
C:\Users\saveenr\Documents\WindowsPowerShell\Modules\Visio\2.0.0\Visio.psd1
```

####   <a id="uninstalling-the-module"></a>

