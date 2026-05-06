# Open-VisioDocument

The **Open-VisioDocument** cmdlet opens an existing Visio file from disk and returns the loaded document object. The cmdlet recognizes stencil extensions (`.vss`, `.vssx`, `.vst`, `.vstx`) and opens them as stencil documents; everything else is opened as a regular drawing.

If no Visio application is currently running, the cmdlet starts one automatically.

> **Templates and stencils are different.** Even though both go through this cmdlet, a template (`.vst` / `.vstx`) usually has an empty `Masters` collection of its own. The masters live in companion stencils that Visio auto-loads alongside the template. If you open a template and `Get-VisioMaster -Document $template` comes back empty, see [Templates vs. stencils](#templates-vs-stencils) below.

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

## Templates vs. stencils

`Open-VisioDocument` opens both stencil files and template files, but the two have different content models:

| Extension | Type | `Masters` collection |
| --- | --- | --- |
| `.vss`, `.vssx` | Stencil | Populated. The shapes you see in the stencil window are direct members. |
| `.vst`, `.vstx` | Template | Often empty. Templates *reference* one or more companion stencils that Visio auto-loads alongside the template. The masters live on the companion documents, not on the template. |

So if you open `actdir_u.vstx` (the Active Directory template) and find that `$template.Masters` is empty, the masters you actually want are on a companion stencil. Two ways to get to them:

### Open the companion stencil directly

If you know the companion stencil's filename, this is the simplest approach. For the Active Directory shapes, that's `actdir_u.vssx`:

```powershell
$stencil = Open-VisioDocument "actdir_u.vssx"
$g       = Get-VisioMaster -Name "Group" -Document $stencil
```

### Walk `Application.Documents` after opening the template

If you don't know the companion filename, open the template and inspect every document Visio has loaded. The companion stencils will be in there. Look for one whose `Masters` collection is non-empty:

```powershell
$app      = Get-VisioApplication
$template = Open-VisioDocument "actdir_u.vstx"

$app.Documents | ForEach-Object {
    "{0,-30} {1,4} masters" -f $_.Name, $_.Masters.Count
}
```

Once you've identified the right document, pass it to `Get-VisioMaster -Document`:

```powershell
$ad_stencil = $app.Documents | Where-Object { $_.Name -like "actdir*.vssx" } | Select-Object -First 1
$g          = Get-VisioMaster -Name "Group" -Document $ad_stencil
```

## See also

* [Close-VisioDocument](close-visiodocument.md)
* [Get-VisioDocument](get-visiodocument.md)
* [New-VisioDocument](new-visiodocument.md)
* [Save-VisioDocument](save-visiodocument.md)
* [Get-VisioMaster](../master/get-visiomaster.md)
