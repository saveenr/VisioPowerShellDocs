# Shape cells

These cmdlets work with the ShapeSheet of shapes:

```text
New-VisioShapeCells
Get-VisioShapeCells
Set-VisioShapeCells
```

#### Working with shape cells <a id="working-with-shape-cells"></a>

To query the cell values of that shape use Get-VisioShapeCells Note that this cmdlet returns a System.Data.DataTable

Setting cell values First, create a new "ShapeCells" object with **New-VisioShapeCells**. Then set the value of cells on that object. Finally, use **Set-VisioShapeCells** to set the cells.

```text
# First, let's draw a shape on a page

Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

New-VisioApplication
$doc = New-VisioDocument

$basic_u = Open-VisioDocument basic_u.vss
$master = Get-VisioMaster "Rectangle" $basic_u
$shape = New-VisioShape $master 2,2

$cells_dt = Get-VisioShapeCells -Shape $shape 

Write-Host $cells_dt

$new_cells = New-VisioShapeCells
$new_cells.XFormWidth = 2
$new_cells.XFormHeight = 4

Set-VisioShapeCells -Cells $new_cells -Shapes $shape
```

