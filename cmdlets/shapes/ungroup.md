# Split-VisioShape

The **Split-VisioShape** cmdlet ungroups one or more group shapes, returning their members to the page as independent shapes. With no arguments it ungroups whatever is currently selected.

## Syntax

```powershell
Split-VisioShape [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Shape` | `Shape[]` | No | Group shape(s) to ungroup. If omitted, the active selection is used. |

## Examples

### Ungroup the current selection

```powershell
Split-VisioShape
```

### Ungroup specific groups

```powershell
$groups = Get-VisioShape -Name "MyGroup1","MyGroup2"
Split-VisioShape -Shape $groups
```

## See also

* [Join-VisioShape](create-groups.md): the inverse: combine shapes into a group.
* [Examples of Join-VisioShape and Split-VisioShape](examples.md)
