# Remove-VisioCustomProperty

The **Remove-VisioCustomProperty** cmdlet deletes a custom (shape-data) property from one or more shapes by name. With no `-Shape` argument the cmdlet operates on the active selection.

`-Name` is required.

## Syntax

```powershell
Remove-VisioCustomProperty [-Name] <String> [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Name` | `String` | Yes (positional) | Name of the custom property to remove. |
| `-Shape` | `Shape[]` | No | Shapes to operate on. If omitted, the active selection is used. |

## Examples

### Remove a property from the current selection

```powershell
Remove-VisioCustomProperty -Name "foo"
```

Or positionally:

```powershell
Remove-VisioCustomProperty "foo"
```

### Remove a property from specific shapes

```powershell
$shapes = Get-VisioShape
Remove-VisioCustomProperty -Name "obsolete" -Shape $shapes
```

## See also

* [Get-VisioCustomProperty](get-visiocustomproperty.md)
* [Set-VisioCustomProperty](set-visiocustomproperty.md)
* [Examples](examples.md)
