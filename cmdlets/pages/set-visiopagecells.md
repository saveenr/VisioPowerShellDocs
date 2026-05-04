# Set-VisioPageCells

The **Set-VisioPageCells** cmdlet writes a `PageCells` object (or an array of them) to the PageSheet of one or more pages. Use it together with [New-VisioPageCells](new-visiopagecells.md), which constructs the cells object you populate and pass in.

All updates run inside a single undo scope.

## Syntax

```powershell
Set-VisioPageCells [-Cells] <PageCells[]> [-Page <Page[]>]
                   [-BlastGuards] [-TestCircular]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Cells` | `PageCells[]` | Yes (positional) | One or more populated `PageCells` objects to write. A single object is broadcast to every target page; an array is zipped position-for-position and cycles if shorter than the page list. |
| `-Page` | `Page[]` | No | Pages to update. If omitted, the active page is used. |
| `-BlastGuards` | `SwitchParameter` | No | Overwrite cells protected by a `GUARD()` formula. |
| `-TestCircular` | `SwitchParameter` | No | Enable the circular-reference check during the write. |

## Examples

### Update the active page

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

```powershell
Set-VisioPageCells -Cells $cells -BlastGuards -TestCircular
```

## See also

* [New-VisioPageCells](new-visiopagecells.md)
* [PageCells](../pagecells.md)
