# Use VisioAutomation

Sometimes you may need to use types from the underlying `VisioAutomation` library directly, for example to construct a `Core.Point` to pass to a cmdlet, or to read a `Src` from `SrcConstants`.

`Import-Module Visio` already loads the VisioAutomation assemblies into the session as a side effect of loading the binary cmdlet DLL, so the types are reachable via `New-Object` and the type-literal syntax (`[Namespace.Type]`) without a separate `Add-Type` call.

```powershell
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

$p = New-Object VisioAutomation.Core.Point(1, 2)
$r = New-Object VisioAutomation.Core.Rectangle(1, 2, 3, 4)
$pinx_src = [VisioAutomation.Core.SrcConstants]::XFormPinX
```

> **Renames since the 3.x module.** The geometry primitives moved from `VisioAutomation.Geometry` to `VisioAutomation.Core`, and `VisioAutomation.ShapeSheet.SRCConstants` was renamed to `VisioAutomation.Core.SrcConstants` (note the casing). Old scripts that reference the previous names need updating.
