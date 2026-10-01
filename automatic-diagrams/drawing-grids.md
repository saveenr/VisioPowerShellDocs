# Grids

A `GridLayout` places shapes in rows and columns. You choose the master to use, the number of columns and rows and a default cell size, then set the text of each cell and pass the layout to [`Out-VisioApplication`](../cmdlets/visioapplication/out-visioapplication.md).

Unlike a [data table](drawing-data-tables.md), a grid lets you set the width of each column and the height of each row.

```powershell
Import-Module Visio

# Open the stencil that holds the master, and a document to draw in
New-VisioDocument -Stencil 'basic_u.vss' | Out-Null
$stencil = Get-VisioDocument 'basic_u*'
$rectangle = Get-VisioMaster 'Rectangle' $stencil

# 3 columns, 2 rows, default cell size 1.5 x 0.5 inches
$cellsize = New-Object VisioAutomation.Core.Size(1.5, 0.5)
$grid = New-Object VisioAutomation.Models.Layouts.Grid.GridLayout -ArgumentList 3, 2, $cellsize, $rectangle

$grid.Origin = New-Object VisioAutomation.Core.Point(1, 5)
$grid.RowDirection = [VisioAutomation.Models.Layouts.Grid.RowDirection]::TopToBottom
$grid.Columns[1].Width = 3

$grid.GetNode(0, 0).Text = 'A1'
$grid.GetNode(1, 0).Text = 'B1'
$grid.GetNode(0, 1).Text = 'A2'

$grid | Out-VisioApplication
```

This draws six rectangles on the current page. The middle column is 3 inches wide and the others are 1.5; `A1`, `B1` and `A2` have text and the other cells are empty.

## Notes

* `GridLayout` needs an `IVisio.Master` object, not a master name. Open the stencil (`New-VisioDocument -Stencil`) and look the master up with `Get-VisioMaster`, passing the stencil document as the second argument. An open stencil document keeps its file extension and is named `BASIC_U.vssx`, which is why the example finds it with the pattern `basic_u*`.
* `GetNode(column, row)` returns the cell; set its `Text`, and optionally `Cells` or `Draw` (set `Draw` to `$false` to skip a cell). Columns and rows are counted from zero.
* `$grid.Columns[i].Width` and `$grid.Rows[i].Height` override the default size for one column or row. They must be greater than zero.
* `CellSpacing` (default 0.5 x 0.25 inches) sets the gaps. `ColumnDirection` (`LeftToRight`, the default, or `RightToLeft`) and `RowDirection` (`BottomToTop`, the default, or `TopToBottom`) set which way the grid grows from `Origin`.
* `Out-VisioApplication` calls `PerformLayout()` for you, and draws the grid on the **current page**. You do not need to call either yourself.

For the object model and the C# API, see [Layouts](https://saveenr.gitbook.io/visioautomation/models/layouts) in the VisioAutomation docs.
