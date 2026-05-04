# New-VisioHyperlink

The **New-VisioHyperlink** cmdlet attaches a hyperlink to one or more shapes. Only `-Address` is required; everything else is optional metadata that maps to the corresponding `Hyperlink` ShapeSheet cells.

## Syntax

```powershell
New-VisioHyperlink -Address <String>
                   [-Description <String>] [-SubAddress <String>]
                   [-ExtraInfo <String>] [-Frame <String>] [-SortKey <String>]
                   [-NewWindow <Boolean>] [-Default <Boolean>] [-Invisible <Boolean>]
                   [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Address` | `String` | Yes | The hyperlink target (URL, file path, etc.). |
| `-Description` | `String` | No | Human-readable description shown to the user. |
| `-SubAddress` | `String` | No | Sub-target (e.g. a page name or a bookmark within `-Address`). |
| `-ExtraInfo` | `String` | No | Extra parameters appended to the URL. |
| `-Frame` | `String` | No | Target frame for browser navigation. |
| `-SortKey` | `String` | No | Sort key when a shape has multiple hyperlinks. |
| `-NewWindow` | `Boolean` | No | If `$true`, opens the link in a new window. |
| `-Default` | `Boolean` | No | If `$true`, marks this as the default hyperlink for the shape. |
| `-Invisible` | `Boolean` | No | If `$true`, the hyperlink is present but not surfaced in the UI. |
| `-Shape` | `Shape[]` | No | Shapes to attach the hyperlink to. If omitted, the active selection is used. |

## Examples

### Attach a hyperlink to the current selection

```powershell
New-VisioHyperlink -Address "http://www.microsoft.com"
```

### Attach a hyperlink with a description and a sub-address

```powershell
New-VisioHyperlink -Address "https://learn.microsoft.com" `
                   -SubAddress "office/visio" `
                   -Description "Visio docs"
```

### Attach a hyperlink to specific shapes

```powershell
$shapes = Get-VisioShape
New-VisioHyperlink -Address "https://example.com" -Shape $shapes[0],$shapes[2]
```

## See also

* [Get-VisioHyperlink](get-visiohyperlink.md)
* [Remove-VisioHyperlink](remove-visiohyperlink.md)
