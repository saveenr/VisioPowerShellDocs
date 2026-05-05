# New-VisioPageCells

The **New-VisioPageCells** cmdlet creates a blank `PageCells` object whose properties map to ShapeSheet cells on a page's PageSheet (size, margins, scale, layout, print setup, etc.). Set the properties you care about and pass the object to [Set-VisioPageCells](set-visiopagecells.md) to apply it.

The cmdlet does not modify the document; it only constructs an in-memory cells object.

## Syntax

```powershell
New-VisioPageCells [-Count <Int32>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Count` | `Int32` | No | If supplied, returns an array of `Count` empty `PageCells` objects. If omitted, returns a single object. |

## Examples

### Create one PageCells object

```powershell
$cells = New-VisioPageCells
$cells.PageWidth  = 11
$cells.PageHeight = 8.5
Set-VisioPageCells -Cells $cells
```

### Create several at once

Use `-Count` to get an array of empty `PageCells` objects, one per page you intend to update.

```powershell
$pages    = Get-VisioPage
$allcells = New-VisioPageCells -Count $pages.Count

foreach ($i in 0..($pages.Count - 1)) {
    $allcells[$i].PageWidth  = 11
    $allcells[$i].PageHeight = 8.5
}

Set-VisioPageCells -Cells $allcells -Page $pages
```

### Discover the available properties

```powershell
$cells = New-VisioPageCells
$cells | Select-Object *
```

## See also

* [Set-VisioPageCells](set-visiopagecells.md)
* [PageCells](../pagecells.md)
