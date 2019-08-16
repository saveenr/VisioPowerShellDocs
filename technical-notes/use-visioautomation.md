# Use VisioAutomation

Sometimes you may need to directly use types in the VisioAutomation assembly. The sample below shows you how to load it into your PowwerShell session

```text
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

import-module Visio

# Load the needed DLLs
$sc = Get-VisioScriptingClient
$sc.Assemblies | %{ Add-Type -Path $_ }

$p = New-Object VisioAutomation.Geometry.Point(1,2)
$r = New-Object VisioAutomation.Geometry.Rectangle(1,2,3,4)
$pinx_src = [VisioAutomation.ShapeSheet.SRCConstants]::XFormPinX
```

