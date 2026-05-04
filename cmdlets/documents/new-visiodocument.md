# New-VisioDocument

The **New-VisioDocument** cmdlet creates a new Visio document. With no arguments it produces a blank drawing; pass `-Template` to start from a specific template file, and `-Stencil` to open one or more stencil documents alongside the new document.

If no Visio application is currently running, the cmdlet starts one automatically.

## Syntax

```powershell
New-VisioDocument [-Template <String>] [-Stencil <String[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Template` | `String` | No | Path to a Visio template file (`.vst`, `.vstx`) to base the new document on. |
| `-Stencil` | `String[]` | No | One or more stencil files (`.vss`, `.vssx`) to open after creating the document. |

## Examples

### Create a new blank document

```powershell
$d = New-VisioDocument
```

### Create a document with a specific template

```powershell
$d = New-VisioDocument -Template "MyTemplate.vstx"
```

### Create a document with stencils preloaded

```powershell
$d = New-VisioDocument -Stencil "basic_u.vss","arrows.vss"
```

## See also

* [Close-VisioDocument](close-visiodocument.md)
* [Get-VisioDocument](get-visiodocument.md)
* [Open-VisioDocument](open-visiodocument.md)
* [Save-VisioDocument](save-visiodocument.md)
