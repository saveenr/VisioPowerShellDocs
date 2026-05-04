# Remove-VisioHyperlink

The **Remove-VisioHyperlink** cmdlet deletes a hyperlink from one or more shapes by its zero-based index. With no `-Shape` argument the cmdlet operates on the active selection.

`-Index` is required.

## Syntax

```powershell
Remove-VisioHyperlink [-Index] <Int32> [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Index` | `Int32` | Yes (positional) | Zero-based index of the hyperlink to remove. |
| `-Shape` | `Shape[]` | No | Shapes to operate on. If omitted, the active selection is used. |

## Examples

### Remove the first hyperlink from the active selection

```powershell
Remove-VisioHyperlink -Index 0
```

### Remove the third hyperlink

```powershell
Remove-VisioHyperlink -Index 2
```

### Remove a hyperlink from specific shapes

```powershell
$shapes = Get-VisioShape
Remove-VisioHyperlink -Index 0 -Shape $shapes[0]
```

## See also

* [Get-VisioHyperlink](get-visiohyperlink.md)
* [New-VisioHyperlink](new-visiohyperlink.md)
