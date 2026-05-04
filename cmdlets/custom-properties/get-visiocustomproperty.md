# Get-VisioCustomProperty

The **Get-VisioCustomProperty** cmdlet returns the custom (shape-data) properties attached to one or more shapes. Result is a dictionary keyed by shape; each value is a dictionary of property-name to `CustomPropertyCells`. Cells are returned as **formulas**.

With no `-Shape` argument the cmdlet reads the active selection.

## Syntax

```powershell
Get-VisioCustomProperty [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Shape` | `Shape[]` | No | Shapes to inspect. If omitted, the active selection is used. |

## Examples

### Read the custom properties on the current selection

```powershell
$props = Get-VisioCustomProperty
foreach ($shape in $props.Keys) {
    foreach ($name in $props[$shape].Keys) {
        $cp = $props[$shape][$name]
        Write-Host "$($shape.NameU).$name = $($cp.Value)"
    }
}
```

### End-to-end: drop a shape, set properties, read them back

```powershell
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

$app          = New-VisioApplication
$doc          = New-VisioDocument
$stencil_net  = Open-VisioDocument "Basic Network Diagram.vst"
$stencil_comp = Open-VisioDocument "Computers and Monitors.vss"

$pc_master = Get-VisioMaster "PC" -Document $stencil_comp
$shapes    = New-VisioShape -Master $pc_master -Position (New-VisioPoint 2.2 6.8)

Set-VisioText "Some Text..." -Shape $shapes
Set-VisioCustomProperty -Name "prop1" -Value "val1" -Shape $shapes
Set-VisioCustomProperty -Name "prop2" -Value "val2" -Shape $shapes

$dict = Get-VisioCustomProperty -Shape $shapes
foreach ($shape in $dict.Keys) {
    foreach ($name in $dict[$shape].Keys) {
        $cp = $dict[$shape][$name]
        Write-Host "--------------------------------------"
        Write-Host "Name      $name"
        Write-Host "Value     $($cp.Value)"
        Write-Host "Prompt    $($cp.Prompt)"
        Write-Host "Label     $($cp.Label)"
        Write-Host "Format    $($cp.Format)"
        Write-Host "Type      $($cp.Type)"
    }
}
```

## See also

* [Set-VisioCustomProperty](set-visiocustomproperty.md)
* [Remove-VisioCustomProperty](remove-visiocustomproperty.md)
* [Examples](examples.md)
