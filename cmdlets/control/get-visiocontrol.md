# Get-VisioControl

The `Get-VisioControl` cmdlet reads the control handles defined on one or more shapes. The result is a dictionary keyed by shape; each value is a list of `ControlCells` objects (one per handle). Cell values come back as **formulas**.

### Read controls from the current selection

When `-Shape` is omitted, the cmdlet reads the active selection.

```powershell
$dict = Get-VisioControl

foreach ($shape in $dict.Keys) {
    $controls = $dict[$shape]
    Write-Host "$($shape.NameU) has $($controls.Count) control handle(s)"
}
```

### Read controls from specific shapes

```powershell
$shapes = Get-VisioShape
$dict   = Get-VisioControl -Shape $shapes[0],$shapes[2]
```

### Inspect a control handle's cells

```powershell
$dict     = Get-VisioControl
$shape    = $dict.Keys | Select-Object -First 1
$controls = $dict[$shape]

$controls[0]   # ControlCells: X, Y, XBehavior, YBehavior, XDynamics, YDynamics, CanGlue, Tip
```

### See also

* [New-VisioControl](new-visiocontrol.md)
* [Remove-VisioControl](remove-visiocontrol.md)
