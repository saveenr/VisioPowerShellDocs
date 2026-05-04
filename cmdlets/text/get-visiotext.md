# Get-VisioText

The **Get-VisioText** cmdlet returns the text of one or more shapes as a list of strings. With no `-Shape` argument the cmdlet reads the active selection.

## Syntax

```powershell
Get-VisioText [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Shape` | `Shape[]` | No | Shapes to read from. If omitted, the active selection is used. |

## Examples

### Read the text of the current selection

```powershell
$texts = Get-VisioText
```

### Read the text of specific shapes

```powershell
$shapes = Get-VisioShape
$texts  = Get-VisioText -Shape $shapes[0],$shapes[2]
```

### Print every shape's text

```powershell
foreach ($shape in Get-VisioShape) {
    $text = Get-VisioText -Shape $shape
    Write-Host "$($shape.NameU): $text"
}
```

## See also

* [Set-VisioText](set-visiotext.md)
