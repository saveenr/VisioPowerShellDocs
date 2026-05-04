# Set-VisioShapeCells for text

```powershell
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

$doc     = New-VisioDocument
$basic_u = Open-VisioDocument "basic_u.vss"
$master  = Get-VisioMaster "Rectangle" -Document $basic_u
$shape   = New-VisioShape -Master $master -Position (New-VisioPoint 2 2)

$font   = $doc.Fonts["Segoe UI"]
$fontid = $font.ID

$shape_cells = New-VisioShapeCells
$shape_cells.CharFont = $font.ID
$shape_cells.CharSize = "14pt"
Set-VisioShapeCells -Cells $shape_cells -Shape $shape
```
