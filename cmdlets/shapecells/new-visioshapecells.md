# New-VisioShapeCells

The **New-VisioShapeCells** cmdlet creates a blank `ShapeCells` object whose properties map to ShapeSheet cells on a shape (size, fill, line, character formatting, and many others). Set the properties you care about and pass the object to `Set-VisioShapeCells` to apply it &mdash; or to [New-VisioShape `-Cells`](../shapes/new-visioshape.md) to apply it at drop time.

The cmdlet does not modify the document &mdash; it only constructs an in-memory cells object.

## Syntax

```powershell
New-VisioShapeCells [-Count <Int32>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Count` | `Int32` | No | If supplied, returns an array of `Count` empty `ShapeCells` objects. If omitted, returns a single object. |

## Examples

### Create one ShapeCells object

```powershell
$cells = New-VisioShapeCells
$cells.XFormWidth     = 2
$cells.XFormHeight    = 1
$cells.FillForeground = "rgb(255,0,0)"
Set-VisioShapeCells -Cells $cells -Shape $shape
```

### Create several at once

Use `-Count` to get an array of empty `ShapeCells` objects, one per shape you intend to update.

```powershell
$shapes   = Get-VisioShape
$allcells = New-VisioShapeCells -Count $shapes.Count

foreach ($i in 0..($shapes.Count - 1)) {
    $allcells[$i].FillPattern = $i
}

Set-VisioShapeCells -Cells $allcells -Shape $shapes
```

### Discover the available properties

`ShapeCells` exposes many properties &mdash; size and position (`XFormWidth`, `PinX`, ...), fill and line (`FillForeground`, `LineWeight`, ...), character formatting (`CharFont`, `CharSize`, ...), and more.

```powershell
$cells = New-VisioShapeCells
$cells | Select-Object *
```

## See also

* [Shape cells](working-with-shape-cells.md) &mdash; end-to-end query/update example.
* [Format shapes with cells](../../basics/format-shapes-with-cells.md)
* [New-VisioShape `-Cells`](../shapes/new-visioshape.md) &mdash; apply ShapeCells at drop time.
