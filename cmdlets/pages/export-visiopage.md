# Export-VisioPage

The **Export-VisioPage** cmdlet exports a single page to an image file. The output format is inferred from the filename extension. With no `-Page` argument the cmdlet exports the active page; pass `-Page` to export a specific one.

`-Filename` is required and positional. The cmdlet exports **one** page per call; to export every page in a document, loop over `Get-VisioPage`.

## Syntax

```powershell
Export-VisioPage [-Filename] <String> [-Page <Page>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Filename` | `String` | Yes (positional) | Output path. Format is inferred from the extension (PNG, JPG, SVG, etc.). |
| `-Page` | `Page` | No | The page to export. If omitted, the active page is used. |

## Examples

### Export the active page as a PNG

```powershell
Export-VisioPage "d:\foo.png"
```

### Export a specific page

```powershell
$page = Get-VisioPage "Settings"
Export-VisioPage "d:\settings.png" -Page $page
```

### Export every page in the active document

The cmdlet handles one page at a time, so loop:

```powershell
foreach ($page in Get-VisioPage) {
    Export-VisioPage "d:\$($page.NameU).png" -Page $page
}
```

## See also

* [Get-VisioPage](get-visiopage.md)
* [Export-VisioShape](../shapes/export-visioshape.md): export shape selections instead of whole pages.
