# Open-VisioDocument

The **Open-VisioDocument** cmdlet opens an existing Visio file from disk and returns the loaded document object. The cmdlet recognizes stencil extensions (`.vss`, `.vssx`, `.vst`, `.vstx`) and opens them as stencil documents; everything else is opened as a regular drawing.

If no Visio application is currently running, the cmdlet starts one automatically.

## Syntax

```powershell
Open-VisioDocument [-Filename] <String>
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Filename` | `String` | Yes (positional) | Path to the file to open. Stencil extensions are detected and opened as stencils. |

## Examples

### Open a drawing

```powershell
$doc = Open-VisioDocument "d:\foo.vsd"
```

### Open a stencil

```powershell
$basic = Open-VisioDocument "basic_u.vss"
$rect_m = Get-VisioMaster "Rectangle" -Document $basic
```

### Filename can be passed positionally

```powershell
Open-VisioDocument "C:\drawings\diagram.vsdx"
```

## See also

* [Close-VisioDocument](close-visiodocument.md)
* [Get-VisioDocument](get-visiodocument.md)
* [New-VisioDocument](new-visiodocument.md)
* [Save-VisioDocument](save-visiodocument.md)
* [Get-VisioMaster](../master/get-visiomaster.md)
