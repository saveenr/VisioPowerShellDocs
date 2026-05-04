# Set-VisioUserDefinedCell

The **Set-VisioUserDefinedCell** cmdlet adds or updates a user-defined cell on one or more shapes. With no `-Shape` argument the cmdlet operates on the active selection.

`-Name` and `-Value` are required.

## Syntax

```powershell
Set-VisioUserDefinedCell [-Name] <String> [-Value] <String>
                         [-Prompt <String>] [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Name` | `String` | Yes (positional 0) | Name of the user-defined cell. |
| `-Value` | `String` | Yes (positional 1) | Cell value (a ShapeSheet formula string). |
| `-Prompt` | `String` | No | Optional prompt / description shown alongside the cell. |
| `-Shape` | `Shape[]` | No | Shapes to update. If omitted, the active selection is used. |

## Examples

### Set a user-defined cell on the current selection

```powershell
Set-VisioUserDefinedCell -Name "foo" -Value "bar"
```

Or positionally:

```powershell
Set-VisioUserDefinedCell "foo" "bar"
```

### Add a prompt

```powershell
Set-VisioUserDefinedCell -Name "Owner" -Value "alice" -Prompt "Email of the owner"
```

### Set a cell on specific shapes

```powershell
$shapes = Get-VisioShape
Set-VisioUserDefinedCell -Name "Region" -Value "EU" -Shape $shapes
```

## See also

* [Get-VisioUserDefinedCell](get-visiouserdefinedcell.md)
* [Remove-VisioUserDefinedCell](remove-visiouserdefinedcell.md)
