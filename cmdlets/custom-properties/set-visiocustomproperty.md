# Set-VisioCustomProperty

The **Set-VisioCustomProperty** cmdlet adds or updates a custom (shape-data) property on one or more shapes. The cmdlet has two forms: pass `-Value` to set the property's value (with optional metadata flags), or pass `-Cells` with a fully-populated `CustomPropertyCells` object for fine-grained control.

With no `-Shape` argument the cmdlet operates on the active selection.

## Syntax

```powershell
# Named-properties form (most common)
Set-VisioCustomProperty [-Name] <String> [-Value] <Object>
                        [-Type <Int32>] [-Label <String>] [-Format <String>]
                        [-Prompt <String>] [-LangId <Int32>] [-SortKey <Int32>]
                        [-Ask <Int32>] [-Calendar <Int32>] [-Invisible <Int32>]
                        [-Shape <Shape[]>]

# CustomPropertyCells form (fine-grained)
Set-VisioCustomProperty [-Name] <String> [-Cells] <CustomPropertyCells>
                        [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-Name` | `String` | Yes (positional 0) | All | Property name. |
| `-Value` | `Object` | Yes (positional 1) | NamedProperties | Property value. Supported types: `String`, `Int32`, `Double`, `Single`, `Boolean`, `DateTime`, `CellValue`. The `Type` cell is inferred from the runtime type. |
| `-Cells` | `CustomPropertyCells` | Yes (positional 1) | Cells | Fully-populated `CustomPropertyCells` object (see `[VisioAutomation.Shapes.CustomPropertyCells]`). |
| `-Type` | `Int32` | No | NamedProperties | Override the inferred property type. `0` = string, `1` = number, `2` = fixed list, `3` = boolean, `4` = variable list, `5` = date, `6` = duration, `7` = currency. |
| `-Label` | `String` | No | NamedProperties | UI label for the property. |
| `-Format` | `String` | No | NamedProperties | Display format string. |
| `-Prompt` | `String` | No | NamedProperties | Tooltip / prompt text. |
| `-LangId` | `Int32` | No | NamedProperties | Locale ID. |
| `-SortKey` | `Int32` | No | NamedProperties | Sort key for ordering properties in the UI. |
| `-Ask` | `Int32` | No | NamedProperties | If `1`, prompts the user when the shape is dropped. |
| `-Calendar` | `Int32` | No | NamedProperties | Calendar ID for date/duration properties. |
| `-Invisible` | `Int32` | No | NamedProperties | If `1`, the property is set but hidden from the UI. |
| `-Shape` | `Shape[]` | No | All | Shapes to update. If omitted, the active selection is used. |

## Examples

### Set a string property

```powershell
Set-VisioCustomProperty -Name "Owner" -Value "Alice"
```

### Set a numeric property

```powershell
Set-VisioCustomProperty -Name "Cost" -Value 12.50 -Format "0.00"
```

### Set a property on specific shapes

```powershell
$shapes = Get-VisioShape
Set-VisioCustomProperty -Name "Region" -Value "EU" -Shape $shapes[0],$shapes[2]
```

### Use the Cells form for full control

```powershell
$cells = New-Object VisioAutomation.Shapes.CustomPropertyCells "ServerName"
$cells.Label  = "Server"
$cells.Prompt = "DNS name of the host"

Set-VisioCustomProperty -Name "ServerName" -Cells $cells
```

## See also

* [Get-VisioCustomProperty](get-visiocustomproperty.md)
* [Remove-VisioCustomProperty](remove-visiocustomproperty.md)
* [Examples](examples.md)
