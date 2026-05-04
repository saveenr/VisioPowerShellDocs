# Get-VisioDocument

The **Get-VisioDocument** cmdlet returns one or more open Visio documents. With no arguments it returns every open document; pass `-ActiveDocument` for the currently active one, or `-Name` to filter by document name (wildcards supported).

## Syntax

```powershell
# All open documents (default) or by name
Get-VisioDocument [-Name <String[]>]

# Just the active document
Get-VisioDocument [-ActiveDocument]
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-Name` | `String[]` | No | docbyname | One or more document names. Wildcards (`*`) are supported. |
| `-ActiveDocument` | `SwitchParameter` | No | active | Return only the active document. |

## Examples

### Get every open document

```powershell
Get-VisioDocument -Name *
```

### Get a document by name

```powershell
Get-VisioDocument -Name "DocumentFoo"
```

### Get the active document

```powershell
Get-VisioDocument -ActiveDocument
```

### Check whether a document is open

`Test-VisioDocument` is the cleanest way to gate on a document being available.

```powershell
if (Test-VisioDocument) {
    # safe to operate on the active document here
}
```

### Switch the active document

Use `Select-VisioDocument` to make a specific document the active one for cmdlets that target the "active document" by default.

```powershell
$doc = Get-VisioDocument -Name "Drawing5"
Select-VisioDocument -Document $doc
```

## See also

* [Close-VisioDocument](close-visiodocument.md)
* [New-VisioDocument](new-visiodocument.md)
* [Open-VisioDocument](open-visiodocument.md)
* [Save-VisioDocument](save-visiodocument.md)
* `Test-VisioDocument`, `Select-VisioDocument` (covered in the [Other cmdlets](../other-cmdlets.md) note).
