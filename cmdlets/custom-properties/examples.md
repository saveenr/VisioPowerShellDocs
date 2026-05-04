# Examples

### Drop a shape, set custom properties, read them back

```powershell
$doc          = New-VisioDocument
$stencil_net  = Open-VisioDocument "Basic Network Diagram.vst"
$stencil_comp = Open-VisioDocument "Computers and Monitors.vss"

$pc_master = Get-VisioMaster -Name "PC" -Document $stencil_comp
$shapes    = New-VisioShape -Master $pc_master -Position (New-VisioPoint 2.2 6.8)
$shape1    = $shapes[0]

Select-VisioShape -Shapes $shape1
$shape1.Text = "Some Text..."

Set-VisioCustomProperty -Name "prop1" -Value "val1"
Set-VisioCustomProperty -Name "prop2" -Value "val2"

$shapedata        = Get-VisioCustomProperty
$props_for_shape1 = $shapedata[$shape1]

foreach ($propname in $props_for_shape1.Keys) {
    $custompropcells = $props_for_shape1[$propname]
    Write-Host "$propname = $($custompropcells.Value.Formula)"
}
```

### Delete a custom property

```powershell
Remove-VisioCustomProperty -Name "prop1" -Shape $shape1
```
