# PageCells

These cmdlets work with the ShapeSheet of pages (page size, margins, scale, layout, print setup, and so on):

* [`New-VisioPageCells`](pages/new-visiopagecells.md): create a blank `PageCells` object to populate.
* `Get-VisioPageCells`: read cells off one or more pages as a DataTable.
* [`Set-VisioPageCells`](pages/set-visiopagecells.md): write a populated `PageCells` to one or more pages.

The pattern is the same as for shape cells: build a cells object, set the properties you care about, write it back.

### Working with page cells

```powershell
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

New-VisioApplication
$doc  = New-VisioDocument
$page = Get-VisioPage -ActivePage

$cells_dt = Get-VisioPageCells -Page $page

Write-Host $cells_dt

$new_cells = New-VisioPageCells
$new_cells.PageHeight = 3
$new_cells.PageWidth  = 6

Set-VisioPageCells -Cells $new_cells -Page $page
```

### Querying multiple pages

```powershell
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

New-VisioApplication
$doc = New-VisioDocument

# The doc already has one page, add four more empty pages
New-VisioPage | Out-Null
New-VisioPage | Out-Null
New-VisioPage | Out-Null
New-VisioPage | Out-Null

$pages = Get-VisioPage

$pages_dt = Get-VisioPageCells -Page $pages

Write-Host $pages_dt
```

## On the C# side

Page-cell-level operations on the C# side go through [`client.ShapeSheet`](https://saveenr.gitbook.io/visioautomation/visio-scripting/shape-sheet) (the same reader / writer pattern that handles ShapeSheet on shapes also applies to a page's PageSheet). See [VisioScripting.Client](https://saveenr.gitbook.io/visioautomation/visio-scripting) for the full facade index.
