# Shape cells

To read the cell values of a shape, use [`Get-VisioShapeCells`](get-visioshapecells.md). It returns a `System.Data.DataTable`.

To write cell values, first create a `ShapeCells` object with [`New-VisioShapeCells`](new-visioshapecells.md). Set the properties you care about. Finally, hand the object to `Set-VisioShapeCells`.

### Working with shape cells

```powershell
# First, let's draw a shape on a page

Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

New-VisioApplication
$doc = New-VisioDocument

$basic_u = Open-VisioDocument "basic_u.vss"
$master  = Get-VisioMaster "Rectangle" -Document $basic_u
$shape   = New-VisioShape -Master $master -Position (New-VisioPoint 2 2)

$cells_dt = Get-VisioShapeCells -Shape $shape

Write-Host $cells_dt

$new_cells = New-VisioShapeCells
$new_cells.XFormWidth  = 2
$new_cells.XFormHeight = 4

Set-VisioShapeCells -Cells $new_cells -Shape $shape
```
