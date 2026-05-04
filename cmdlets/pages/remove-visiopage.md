# Remove-VisioPage

The **Remove-VisioPage** cmdlet deletes one or more pages from the active document. With no arguments it deletes the active page. Pages can be passed via `-Page` (named or pipeline). Use `-Renumber` to renumber the remaining pages so default `Page-N` names stay sequential.

## Syntax

```powershell
Remove-VisioPage [-Page <Page[]>] [-Renumber]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Page` | `Page[]` | No (pipeline) | The page or pages to delete. Accepts pipeline input. If omitted, the active page is deleted. |
| `-Renumber` | `SwitchParameter` | No | Renumber the remaining pages after deletion. |

## Examples

### Delete the active page

```powershell
Remove-VisioPage
```

### Delete specific pages

```powershell
$pages = Get-VisioPage

# delete the first page
Remove-VisioPage -Page $pages[0]

# delete the first and fourth pages
Remove-VisioPage -Page $pages[0],$pages[3]
```

### Delete all pages

```powershell
$pages = Get-VisioPage
Remove-VisioPage -Page $pages
```

### Delete all pages with names matching a wildcard via the pipeline

```powershell
Get-VisioPage "*backup*" | Remove-VisioPage
```

### Delete and renumber the remaining pages

```powershell
Remove-VisioPage -Page $pages[1] -Renumber
```

## See also

* [Get-VisioPage](get-visiopage.md)
* [New-VisioPage](new-visiopage.md)
