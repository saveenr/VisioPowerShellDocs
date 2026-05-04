# New-VisioShape

The **New-VisioShape** cmdlet creates one or more shapes on the active page. It works in two modes:

* **Drop a master** from a stencil at one or more positions. This is the recommended way to create shapes.
* **Draw a primitive** &mdash; rectangle, oval, line, polyline, or Bezier &mdash; without a master.

The cmdlet returns the shapes it created.

## Syntax

The cmdlet has six parameter sets, one for each shape kind. Pick the syntax that matches what you're creating.

```powershell
# Drop master(s)
New-VisioShape [-Master] <Master[]> -Position <Point[]> [-Cells <ShapeCells[]>]

# Draw a rectangle
New-VisioShape [-Rectangle] [-BoundingBox] <Rectangle> [-Cells <ShapeCells[]>]

# Draw an oval
New-VisioShape [-Oval] [-BoundingBox] <Rectangle> [-Cells <ShapeCells[]>]

# Draw a line
New-VisioShape [-Line] -From <Point> -To <Point> [-Cells <ShapeCells[]>]

# Draw a polyline
New-VisioShape [-Polyline] [-Points] <Point[]> [-Cells <ShapeCells[]>]

# Draw a Bezier curve
New-VisioShape [-Bezier] [-Points] <Point[]> [-Cells <ShapeCells[]>]
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-Master` | `Master[]` | Yes | Drop master | The master(s) to drop. If `-Position` has more entries than `-Master`, the masters are reused (cycled). |
| `-Position` | `Point[]` | Yes | Drop master | Where each master is dropped. |
| `-Rectangle` | `SwitchParameter` | Yes | Rectangle | Selects rectangle mode. |
| `-Oval` | `SwitchParameter` | Yes | Oval | Selects oval mode. |
| `-BoundingBox` | `Rectangle` | Yes | Rectangle, Oval | Bounds of the rectangle or oval (`Left, Bottom, Right, Top`). Build with `New-VisioRectangle`. |
| `-Line` | `SwitchParameter` | Yes | Line | Selects line mode. |
| `-From` | `Point` | Yes | Line | Line start point. |
| `-To` | `Point` | Yes | Line | Line end point. |
| `-Polyline` | `SwitchParameter` | Yes | Polyline | Selects polyline mode. Requires at least 2 points. |
| `-Bezier` | `SwitchParameter` | Yes | Bezier | Selects Bezier mode. Requires at least 4 points (each cubic segment uses two endpoints and two control points). |
| `-Points` | `Point[]` | Yes | Polyline, Bezier | The points the polyline or Bezier passes through. |
| `-Cells` | `ShapeCells[]` | No | All | ShapeSheet cells to apply to the new shape(s). A single object applies to every shape; an array is zipped position-for-position and cycles if shorter than the shape count. |

## Examples

### Drop a master at a single point

```powershell
$basic_u = Open-VisioDocument "basic_u.vss"
$rect_m  = Get-VisioMaster "Rectangle" -Document $basic_u
$shape   = New-VisioShape -Master $rect_m -Position (New-VisioPoint 4 5)
```

### Drop a master at multiple points

Pass an array of points to drop the same master at each location.

```powershell
$basic_u = Open-VisioDocument "basic_u.vss"
$rect_m  = Get-VisioMaster "Rectangle" -Document $basic_u
$points  = @(
    New-VisioPoint 4 5
    New-VisioPoint 6 1
    New-VisioPoint 0 0
)
$shapes = New-VisioShape -Master $rect_m -Position $points
```

### Drop multiple masters at multiple points

Pass arrays of equal length for `-Master` and `-Position`. Master `[i]` is dropped at point `[i]`.

```powershell
$basic_u = Open-VisioDocument "basic_u.vss"
$masters = Get-VisioMaster -Name "Rectangle","Triangle","Circle" -Document $basic_u
$points  = @(
    New-VisioPoint 4 5
    New-VisioPoint 6 1
    New-VisioPoint 0 0
)
$shapes = New-VisioShape -Master $masters -Position $points
```

### Apply ShapeCells while dropping

Pass `-Cells` to set ShapeSheet cells on the dropped shapes in the same step. When `-Cells` is a single object, it applies to every shape; when it is an array, the shape at index `i` gets the cells at index `i % cells.Length` &mdash; so a shorter array cycles.

```powershell
$cells = New-VisioShapeCells
$cells.XFormWidth     = 2
$cells.XFormHeight    = 1
$cells.FillForeground = "rgb(255,0,0)"

$basic_u = Open-VisioDocument "basic_u.vss"
$rect_m  = Get-VisioMaster "Rectangle" -Document $basic_u
$points  = @(
    New-VisioPoint 4 5
    New-VisioPoint 6 1
)
$shapes = New-VisioShape -Master $rect_m -Position $points -Cells $cells
```

See [Format shapes with cells](../../basics/format-shapes-with-cells.md) for a fuller treatment, including per-shape formatting.

### Draw a rectangle or oval

Use `-Rectangle` or `-Oval` with a bounding box (`Left, Bottom, Right, Top`).

```powershell
$rect = New-VisioShape -Rectangle (New-VisioRectangle 1 1 4 3)
$oval = New-VisioShape -Oval      (New-VisioRectangle 5 1 8 3)
```

### Draw a line

Use `-Line` with `-From` and `-To`.

```powershell
$line = New-VisioShape -Line `
    -From (New-VisioPoint 0 0) `
    -To   (New-VisioPoint 4 4)
```

### Draw a polyline or Bezier

Use `-Polyline` or `-Bezier` with `-Points`. A polyline needs at least 2 points; a Bezier needs at least 4 (each cubic segment uses two endpoints and two control points).

```powershell
$points = @(
    New-VisioPoint 0 0
    New-VisioPoint 1 2
    New-VisioPoint 3 1
    New-VisioPoint 5 4
)
$polyline = New-VisioShape -Polyline -Points $points
$bezier   = New-VisioShape -Bezier   -Points $points
```

## See also

* [Drop shape masters](../../basics/drop-masters.md)
* [Draw basic shapes](../../basics/draw-basic-shapes.md)
* [Format shapes with cells](../../basics/format-shapes-with-cells.md)
* `New-VisioPoint`, `New-VisioRectangle`, `Get-VisioMaster`, `New-VisioShapeCells`
