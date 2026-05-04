# Remove-VisioShape

The **Remove-VisioShape** cmdlet deletes shapes from the active page. With no arguments it deletes the current selection; pass `-Shape` to delete specific shapes.

## Syntax

```powershell
Remove-VisioShape [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Shape` | `Shape[]` | No | Shapes to delete. If omitted, the current selection is deleted. |

## Examples

### Delete the current selection

```powershell
Remove-VisioShape
```

### Delete specific shapes

```powershell
$shapes = Get-VisioShape

# delete the first shape
Remove-VisioShape -Shape $shapes[0]

# delete the first and third shapes
Remove-VisioShape -Shape $shapes[0],$shapes[2]
```

### Delete all shapes on the page

```powershell
Select-VisioShape All
Remove-VisioShape
```

## See also

* [New-VisioShape](new-visioshape.md)
* [Select-VisioShape](selecting-shapes.md)
