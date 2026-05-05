# Save-VisioDocument

The **Save-VisioDocument** cmdlet saves a Visio document to disk. With no arguments it saves the active document to its current path (Save). Pass a filename to save under a new path (Save As). Use `-Document` to save a document other than the active one.

## Syntax

```powershell
Save-VisioDocument [[-Filename] <String>] [-Document <Document>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Filename` | `String` | No (positional) | If supplied, performs Save As to this path. If omitted, saves the document at its existing path. |
| `-Document` | `Document` | No | The document to save. If omitted, the active document is saved. |

## Examples

### Save the active document

```powershell
Save-VisioDocument
```

### Save As: save the active document to a new path

```powershell
Save-VisioDocument "d:\foo.vsd"
```

### Save a specific document

```powershell
$doc = Get-VisioDocument -Name "Drawing5"
Save-VisioDocument -Document $doc
```

## See also

* [Close-VisioDocument](close-visiodocument.md)
* [Get-VisioDocument](get-visiodocument.md)
* [New-VisioDocument](new-visiodocument.md)
* [Open-VisioDocument](open-visiodocument.md)
