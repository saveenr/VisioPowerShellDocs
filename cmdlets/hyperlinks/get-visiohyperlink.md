# Get-VisioHyperlink

The **Get-VisioHyperlink** cmdlet returns the hyperlinks attached to one or more shapes. The result is a dictionary keyed by shape; each value is the list of `HyperlinkCells` records attached to that shape (a shape may have multiple hyperlinks). With no `-Shape` argument the cmdlet reads the active selection.

## Syntax

```powershell
Get-VisioHyperlink [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Shape` | `Shape[]` | No | Shapes to inspect. If omitted, the active selection is used. |

## Examples

### Read the hyperlinks on the current selection

```powershell
$dict = Get-VisioHyperlink
foreach ($shape in $dict.Keys) {
    foreach ($h in $dict[$shape]) {
        Write-Host "$($shape.NameU) -> $($h.Address)"
    }
}
```

### Sample output

```
Address     : "http://www.microsoft.com"
Default     : FALSE
Description :
ExtraInfo   :
Frame       :
Invisible   : FALSE
NewWindow   : FALSE
SortKey     : ""
SubAddress  :
ShapeID     : 1

Address     : "http://www.google.com"
Default     : FALSE
Description :
ExtraInfo   : ""
Frame       :
Invisible   : FALSE
NewWindow   : FALSE
SortKey     : ""
SubAddress  :
ShapeID     : 1
```

## See also

* [New-VisioHyperlink](new-visiohyperlink.md)
* [Remove-VisioHyperlink](remove-visiohyperlink.md)
