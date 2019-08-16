# Lay out shapes

Visio has a feature on the DESIGN tab that can re-layout objects on a page.

![](../.gitbook/assets/snap00010.png)

```text
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

import-module Visio

New-VisioDocument

$shape_a = New-VisioShape Rectangle 5,7,6,8
Set-VisioText "A"
$shape_b = New-VisioShape Rectangle 3,5,4,6
Set-VisioText "B"
$shape_c = New-VisioShape Rectangle 7,5,8,6
Set-VisioText "C"

Connect-VisioShape $shape_a $shape_b
Connect-VisioShape $shape_a $shape_c

$sc = Get-VisioScriptingClient
$sc.Assemblies | %{ Add-Type -Path $_ }

$ls = New-Object VisioAutomation.Models.LayoutStyles.FlowchartLayoutStyle
$ls.AvenueSizeX = 1
$ls.AvenueSizeY = 0.5

Format-VisioPage -LayoutStyle $ls
```

![](../.gitbook/assets/snap00012.png)

