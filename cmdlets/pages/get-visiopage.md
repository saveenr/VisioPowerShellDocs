# Get-VisioPage

The **Get-VisioPage** cmdlet returns one or more pages from a Visio document. With no arguments it returns every page in the active document; pass `-ActivePage` for the currently-active one, `-Name` to filter by page name (wildcards supported), or `-ID` to look up pages by their numeric Visio ID. The optional `-Document` switches the source document away from the active one.

## Syntax

```powershell
# All pages (default), or by name
Get-VisioPage [[-Name] <String[]>] [-Document <Document>]

# By Visio page ID
Get-VisioPage [-ID <Int32[]>] [-Document <Document>]

# Just the active page
Get-VisioPage [-ActivePage] [-Document <Document>]
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-Name` | `String[]` | No (positional) | pagebyname | One or more page names. Wildcards (`*`, `?`) are supported. |
| `-ID` | `Int32[]` | No | pagebyid | One or more numeric Visio page IDs. |
| `-ActivePage` | `SwitchParameter` | No | active | Return only the active page. |
| `-Document` | `Document` | No | All | The document to search. If omitted, the active document is used. |

## Examples

### Get every page in the active document

```powershell
$pages = Get-VisioPage
```

### Get a page by name

```powershell
$pages = Get-VisioPage "Page-1"
```

### Find pages by name with wildcards

```powershell
$pages = Get-VisioPage "*foo"
```

### Get the active page

```powershell
$page = Get-VisioPage -ActivePage
```

### Get pages by Visio ID

```powershell
$pages = Get-VisioPage -ID 1,3
```

### Switch the active page

Use `Select-VisioPage` to make a different page the active one.

```powershell
$page = Get-VisioPage "Page-2"
Select-VisioPage -Page $page
```

## See also

* [New-VisioPage](new-visiopage.md)
* [Remove-VisioPage](remove-visiopage.md)
* [Format-VisioPage](format-visiopage.md)
* [Export-VisioPage](export-visiopage.md)
* [Measure-VisioPage](measure-visiopage.md)
