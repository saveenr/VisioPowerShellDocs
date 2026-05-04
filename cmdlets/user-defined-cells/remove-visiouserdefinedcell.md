# Remove-VisioUserDefinedCell

The **Remove-VisioUserDefinedCell** cmdlet deletes a user-defined cell from one or more shapes by name. With no `-Shape` argument the cmdlet operates on the active selection.

`-Name` is required.

## Syntax

```powershell
Remove-VisioUserDefinedCell [-Name] <String> [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Name` | `String` | Yes (positional) | Name of the user-defined cell to remove. |
| `-Shape` | `Shape[]` | No | Shapes to operate on. If omitted, the active selection is used. |

## Examples

### Remove a cell from the current selection

```powershell
Remove-VisioUserDefinedCell -Name "Foo"
```

Or positionally:

```powershell
Remove-VisioUserDefinedCell "Foo"
```

### Remove a cell from specific shapes

```powershell
$shapes = Get-VisioShape
Remove-VisioUserDefinedCell -Name "obsolete" -Shape $shapes
```

## See also

* [Get-VisioUserDefinedCell](get-visiouserdefinedcell.md)
* [Set-VisioUserDefinedCell](set-visiouserdefinedcell.md)
