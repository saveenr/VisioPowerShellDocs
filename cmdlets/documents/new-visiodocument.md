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
| `-Template` | `String` | No | Path to a Visio template file (`.vst`, `.vstx`) to base the new document on. A stencil file (`.vss`, `.vssx`) is not a template and fails with an error; use `-Stencil` for those. |
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

The new document gets the template's page setup, styles and settings, and Visio opens and docks the stencils that belong to the template. For example, `New-VisioDocument -Template "basflo_u.vstx"` gives a landscape drawing with the Basic Flowchart and Cross-Functional Flowchart stencils docked.

> **`-Template` changed in 4.8.0.** In 4.7.3 and earlier, `-Template` created a blank drawing and opened the template file as a separate docked stencil (an empty one in Visio 2013 and later), so the new document was not based on the template. Passing a stencil to `-Template` failed with an unhelpful error. From 4.8.0, `-Template` creates the document from the template, and a stencil file is rejected with a clear message. If a script relied on the old behavior to open a stencil, use `-Stencil` instead ([#229](https://github.com/saveenr/VisioAutomation/issues/229)).

### Create a document with stencils preloaded

```powershell
$d = New-VisioDocument -Stencil "basic_u.vss","arrows.vss"
```

## See also

* [Close-VisioDocument](close-visiodocument.md)
* [Get-VisioDocument](get-visiodocument.md)
* [Open-VisioDocument](open-visiodocument.md)
* [Save-VisioDocument](save-visiodocument.md)
