# Select-VisioShape

The **Select-VisioShape** cmdlet changes the active selection in Visio. It works in two modes &mdash; either pass an explicit list of shapes, or pass a high-level operation (`SelectAll`, `SelectNone`, `InvertSelection`).

## Syntax

```powershell
# Select specific shapes
Select-VisioShape [-Shapes] <Shape[]>

# Apply a high-level selection operation
Select-VisioShape [-SelectionOperation] <ShapeSelectionOperation>
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-Shapes` | `Shape[]` | Yes (positional) | SelectByShapes | Shapes to select. The list replaces the current selection. |
| `-SelectionOperation` | `ShapeSelectionOperation` | Yes (positional) | SelectByOperation | One of `SelectAll`, `SelectNone`, `InvertSelection`. |

## Examples

### Select all shapes on the active page

```powershell
Select-VisioShape SelectAll
```

### Clear the selection

```powershell
Select-VisioShape SelectNone
```

See [Select-VisioShape (clear selection)](clearing-the-selection.md) for context.

### Invert the selection

```powershell
Select-VisioShape InvertSelection
```

See [Select-VisioShape (invert)](invert-the-selection.md) for context.

### Select specific shape objects

```powershell
$rect_m = Get-VisioMaster "Rectangle" -Document (Open-VisioDocument "basic_u.vss")
$s1 = New-VisioShape -Master $rect_m -Position (New-VisioPoint 0 0)
$s2 = New-VisioShape -Master $rect_m -Position (New-VisioPoint 2 2)
$s3 = New-VisioShape -Master $rect_m -Position (New-VisioPoint 4 4)

Select-VisioShape -Shapes $s1,$s3
```

Positional form also works:

```powershell
Select-VisioShape $s1,$s3
```

## See also

* [Get-VisioShape](enumerate-selected-shapes.md) &mdash; read the current selection.
* [Test-VisioShape](test-visioshape.md) &mdash; check whether anything is selected.
* [Select-VisioShape (clear selection)](clearing-the-selection.md)
* [Select-VisioShape (invert)](invert-the-selection.md)
