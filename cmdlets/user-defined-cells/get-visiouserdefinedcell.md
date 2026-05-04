# Get-VisioUserDefinedCell

The **Get-VisioUserDefinedCell** cmdlet returns the user-defined cells attached to one or more shapes. Result is a dictionary keyed by shape; each value is a dictionary of cell-name to `UserDefinedCellCells` (which holds `Value` and `Prompt` formulas).

With no `-Shape` argument the cmdlet reads the active selection.

## Syntax

```powershell
Get-VisioUserDefinedCell [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Shape` | `Shape[]` | No | Shapes to inspect. If omitted, the active selection is used. |

## Examples

### Read the user-defined cells on the current selection

```powershell
$dict = Get-VisioUserDefinedCell
foreach ($shape in $dict.Keys) {
    foreach ($name in $dict[$shape].Keys) {
        $u = $dict[$shape][$name]
        Write-Host "$($shape.NameU).$name = $($u.Value)"
    }
}
```

### Read the user-defined cells on specific shapes

```powershell
$shapes = Get-VisioShape
$dict   = Get-VisioUserDefinedCell -Shape $shapes[0],$shapes[2]
```

## See also

* [Set-VisioUserDefinedCell](set-visiouserdefinedcell.md)
* [Remove-VisioUserDefinedCell](remove-visiouserdefinedcell.md)
