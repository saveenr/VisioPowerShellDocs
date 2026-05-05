# Connect-VisioShape

The **Connect-VisioShape** cmdlet draws connectors between shapes. `-From` and `-To` accept arrays so you can wire many connections in one call: element `i` of `-From` is connected to element `i` of `-To`. Pass `-Master` to use a specific connector master (e.g. "Dynamic Connector"); omit it for Visio's default connector.

## Syntax

```powershell
Connect-VisioShape [-From] <Shape[]> [-To] <Shape[]> [[-Master] <Master>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-From` | `Shape[]` | Yes (positional 0) | Source shapes. |
| `-To` | `Shape[]` | Yes (positional 1) | Destination shapes. Must be the same length as `-From`. |
| `-Master` | `Master` | No (positional 2) | Connector master to use. If omitted, Visio's default is used. |

## Examples

### Connect two shapes

```powershell
Import-Module Visio

New-VisioApplication
New-VisioDocument

$basic_u  = Open-VisioDocument "basic_u.vss"
$rect_m   = Get-VisioMaster -Name "Rectangle"          -Document $basic_u
$dyncon_m = Get-VisioMaster -Name "Dynamic Connector"  -Document $basic_u

$shape_0 = New-VisioShape -Master $rect_m -Position (New-VisioPoint 2 2)
$shape_1 = New-VisioShape -Master $rect_m -Position (New-VisioPoint 4 4)

Connect-VisioShape -From $shape_0 -To $shape_1 -Master $dyncon_m
```

![](../../.gitbook/assets/snap00005.png)

### Wire many shapes at once

`-From` and `-To` are zipped position-for-position: connector[i] runs from From[i] to To[i].

```powershell
$a = New-VisioShape -Master $rect_m -Position (New-VisioPoint 0 0)
$b = New-VisioShape -Master $rect_m -Position (New-VisioPoint 2 2)
$c = New-VisioShape -Master $rect_m -Position (New-VisioPoint 4 4)
$d = New-VisioShape -Master $rect_m -Position (New-VisioPoint 6 6)

Connect-VisioShape -From $a,$b,$c -To $b,$c,$d -Master $dyncon_m
```

## See also

* [New-VisioShape](new-visioshape.md)
* [Get-VisioMaster](../master/get-visiomaster.md)
