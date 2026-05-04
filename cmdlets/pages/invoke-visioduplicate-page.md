# Copy-VisioPage

The **Copy-VisioPage** cmdlet duplicates a page. By default the duplicate is placed in the same document; pass `-ToDocument` to drop it into a different document instead. With no `-Page` argument the cmdlet duplicates the active page. The new page is returned.

## Syntax

```powershell
Copy-VisioPage [-Page <Page>] [-ToDocument <Document>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Page` | `Page` | No | The page to duplicate. If omitted, the active page is duplicated. |
| `-ToDocument` | `Document` | No | The destination document for the duplicate. If omitted, the duplicate stays in the page's existing document. |

## Examples

### Duplicate the active page

```powershell
$copy = Copy-VisioPage
```

### Duplicate a specific page

```powershell
$page = Get-VisioPage "Page-2"
$copy = Copy-VisioPage -Page $page
```

### Copy a page into another document

```powershell
$src = Get-VisioPage "Source"
$dst = Get-VisioDocument -Name "Other.vsdx"
$copy = Copy-VisioPage -Page $src -ToDocument $dst
```

## See also

* [Get-VisioPage](get-visiopage.md)
* [New-VisioPage](new-visiopage.md)
* [Remove-VisioPage](remove-visiopage.md)
