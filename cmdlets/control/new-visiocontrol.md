# New-VisioControl

The `New-VisioControl` cmdlet adds a control handle to one or more shapes. A control handle is the yellow draggable diamond a user can grab to adjust a shape's geometry.

Every parameter is optional &mdash; in practice you'll always want to supply at least `-X` and `-Y` so the handle has a position. The cell-style parameters take ShapeSheet **formulas** as strings (e.g. `"Width*0.5"`, `"0.25 in"`).

### Add a centered control handle

```powershell
New-VisioControl -X "Width*0.5" -Y "Height*0.5" -Tip "Adjust"
```

### Specify behavior and dynamics

The behavior/dynamics cells use Visio's standard ShapeSheet enumerations expressed as formulas (numeric constants are typical, e.g. `"0"`, `"1"`).

```powershell
New-VisioControl `
    -X         "Width*0.5" `
    -Y         "Height"    `
    -XBehavior "1"         `
    -YBehavior "1"         `
    -XDynamics "1"         `
    -YDynamics "1"         `
    -CanGlue   $false      `
    -Tip       "Top middle"
```

### Add a handle to specific shapes

When `-Shape` is omitted the cmdlet targets the active selection.

```powershell
$shapes = Get-VisioShape
New-VisioControl -X "Width*0.5" -Y "Height*0.5" -Shape $shapes[0],$shapes[1]
```

### See also

* [Get-VisioControl](get-visiocontrol.md)
* [Remove-VisioControl](remove-visiocontrol.md)
