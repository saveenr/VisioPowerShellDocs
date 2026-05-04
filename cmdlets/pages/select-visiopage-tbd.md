# Select-VisioPage

The **Select-VisioPage** cmdlet makes a specific page the active page in the bound Visio application. Subsequent cmdlets that target the active page operate on this page.

`-Page` is required.

## Syntax

```powershell
Select-VisioPage [-Page] <Page>
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Page` | `Page` | Yes (positional) | The page to make active. Must not be `$null`. |

## Examples

### Switch to a page by name

```powershell
$page = Get-VisioPage "Page-2"
Select-VisioPage -Page $page
```

Or positionally:

```powershell
Select-VisioPage (Get-VisioPage "Page-2")
```

### Iterate every page in turn

```powershell
foreach ($page in Get-VisioPage) {
    Select-VisioPage -Page $page
    # ... do something with the active page
}
```

## See also

* [Get-VisioPage](get-visiopage.md) &mdash; locate the page you want to switch to.
* [New-VisioPage](new-visiopage.md)
