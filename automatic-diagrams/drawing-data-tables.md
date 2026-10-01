# Data tables

A `DataTableModel` draws a `System.Data.DataTable` as a grid of rectangles, one per cell, with each value as the shape text. Pass it to [`Out-VisioApplication`](../cmdlets/visioapplication/out-visioapplication.md).

```powershell
Import-Module Visio
New-VisioDocument | Out-Null

$dt = New-Object System.Data.DataTable
[void]$dt.Columns.Add('Name')
[void]$dt.Columns.Add('Role')
[void]$dt.Rows.Add('Alice', 'Owner')
[void]$dt.Rows.Add('Bob', 'Reviewer')

$model = New-Object VisioAutomation.Models.Data.DataTableModel
$model.DataTable = $dt
$model.CellWidth = 1.5
$model.CellHeight = 0.5
$model.CellSpacing = 0.1

$model | Out-VisioApplication
```

This puts four rectangles on the active page, each 1.5 inches wide and 0.5 inches high: `Alice` and `Owner` on the first row, `Bob` and `Reviewer` on the second.

## What to expect

* The table is drawn on the **current page** of the active document, starting at the top left of the page. A Visio application and document must already exist.
* Every column is `CellWidth` wide and every row `CellHeight` high (both default to **1 inch**), with `CellSpacing` (in inches, applied both ways) between cells. To give each column its own width and each row its own height, use a [grid layout](drawing-grids.md).
* `CellWidth` and `CellHeight` take effect in Visio PowerShell releases after 4.7.3, because the bundled library change is unreleased. In 4.7.3 and earlier they have no effect and every cell is 1 x 1 inch; only `CellSpacing` does.
* There is **no header row**. Column names are not drawn; add them as the first data row if you want them.
* A null value is drawn as an empty cell.
* The table needs at least one row.

For the object model and the C# API, see [Data table model](https://saveenr.gitbook.io/visioautomation/models/data-table) in the VisioAutomation docs.
