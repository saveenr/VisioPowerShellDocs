# Remove-VisioControl

The `Remove-VisioControl` cmdlet deletes a control handle from one or more shapes. The handle is identified by its zero-based index within the shape's `Controls` section.

`-Index` is required.

### Remove the first control handle from the active selection

```powershell
Remove-VisioControl -Index 0
```

### Remove the second handle from specific shapes

```powershell
$shapes = Get-VisioShape
Remove-VisioControl -Index 1 -Shape $shapes[0],$shapes[2]
```

### Find an index with Get-VisioControl

```powershell
$dict     = Get-VisioControl
$shape    = $dict.Keys | Select-Object -First 1
$controls = $dict[$shape]

# enumerate handles to find the one you want
for ($i = 0; $i -lt $controls.Count; $i++) {
    Write-Host "$i  tip=$($controls[$i].Tip)"
}

# then remove it
Remove-VisioControl -Index 1 -Shape $shape
```

### See also

* [Get-VisioControl](get-visiocontrol.md)
* [New-VisioControl](new-visiocontrol.md)
