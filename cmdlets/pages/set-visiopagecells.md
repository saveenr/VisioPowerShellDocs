# Set-VisioPageCells

The `Set-VisioPageCells` cmdlet writes a `PageCells` object (or an array of them) to the PageSheet of one or more pages. Use it together with [`New-VisioPageCells`](new-visiopagecells.md), which constructs the cells object you populate and pass in.

All updates run inside a single undo scope.

### Update the active page

When `-Page` is omitted, the cmdlet targets the active page.

```powershell
$cells = New-VisioPageCells
$cells.PageWidth  = 11
$cells.PageHeight = 8.5

Set-VisioPageCells -Cells $cells
```

### Update specific pages

```powershell
$cells = New-VisioPageCells
$cells.PageWidth  = 11
$cells.PageHeight = 8.5

$pages = Get-VisioPage
Set-VisioPageCells -Cells $cells -Page $pages[0],$pages[2]
```

A single `PageCells` is broadcast to every page; an array is zipped position-for-position. If the array is shorter than the page list it cycles (page index `i` uses cells `i % cells.Length`).

### Per-page settings

```powershell
$cells_letter = New-VisioPageCells
$cells_letter.PageWidth  = 11
$cells_letter.PageHeight = 8.5

$cells_a4 = New-VisioPageCells
$cells_a4.PageWidth  = 11.69
$cells_a4.PageHeight = 8.27

$pages = Get-VisioPage
Set-VisioPageCells -Cells $cells_letter,$cells_a4 -Page $pages
```

### Bypass guarded formulas

`-BlastGuards` lets the writer overwrite cells that are protected by a `GUARD()` formula. `-TestCircular` enables the circular-reference check. Both are off by default.

```powershell
Set-VisioPageCells -Cells $cells -BlastGuards -TestCircular
```

### See also

* [New-VisioPageCells](new-visiopagecells.md)
* [PageCells](../pagecells.md)
