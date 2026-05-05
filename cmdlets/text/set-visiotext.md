# Set-VisioText

The **Set-VisioText** cmdlet sets the text of one or more shapes. With no `-Shape` argument the cmdlet operates on the active selection.

`-Text` is required. When updating multiple shapes, pass an array of strings; element `i` is applied to shape `i`. A single string is applied to every target shape.

## Syntax

```powershell
Set-VisioText [-Text] <String[]> [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Text` | `String[]` | Yes (positional) | Text to set. A single string is applied to every shape; an array is zipped position-for-position with the target shapes. |
| `-Shape` | `Shape[]` | No | Shapes to update. If omitted, the active selection is used. |

## Examples

### Set the text on the current selection

```powershell
Set-VisioText "Hello World"
```

### Set the text on a specific shape

```powershell
$shapes = Get-VisioShape
Set-VisioText "Hello" -Shape $shapes[0]
```

### Set different text on multiple shapes

```powershell
$shapes = Get-VisioShape
Set-VisioText "A","B","C" -Shape $shapes[0],$shapes[1],$shapes[2]
```

## See also

* `Get-VisioText` (currently a documentation stub).
* [Set-VisioShapeCells for text](../shapecells/format-text.md): format the text after setting it.
