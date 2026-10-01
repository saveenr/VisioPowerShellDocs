# Get-VisioPage

The **Get-VisioPage** cmdlet returns one or more pages from a Visio document. With no arguments it returns every page in the active document; pass `-ActivePage` for the currently-active one, `-Name` to filter by page name (wildcards supported), `-ID` to look up pages by their numeric Visio page ID, or `-Index` to take pages by their position in the document. The optional `-Document` switches the source document away from the active one.

## Syntax

```powershell
# All pages (default), or by name
Get-VisioPage [[-Name] <String[]>] [-Document <Document>]

# By Visio page ID
Get-VisioPage [-ID <Int32[]>] [-Document <Document>]

# By position in the document (1 is the first page)
Get-VisioPage [-Index <Int32[]>] [-Document <Document>]

# Just the active page
Get-VisioPage [-ActivePage] [-Document <Document>]
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-Name` | `String[]` | No (positional) | pagebyname | One or more page names. Wildcards (`*`, `?`) are supported. |
| `-ID` | `Int32[]` | No | pagebyid | One or more numeric Visio page IDs (`Page.ID`). An ID is not a position: the first page of a new document has ID 0, and a page added later gets the next unused ID. Read IDs from `$page.ID` or from the `PageID` column of `Get-VisioPageCells`. |
| `-Index` | `Int32[]` | No | pagebyindex | One or more positions in the document, counting from 1 (the first page is 1, matching Visio's own page numbering and `Page.Index`). Added in an unreleased change after 4.7.3. |
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

### Get a page by Visio ID

```powershell
$overview = New-VisioPage -Name "Overview"
$same_page = Get-VisioPage -ID $overview.ID
```

### Get pages by position

```powershell
$first = Get-VisioPage -Index 1
$first_and_third = Get-VisioPage -Index 1,3
```

> **`-ID` changed after 4.7.3.** In 4.7.3 and earlier, `-ID` silently treated its numbers as positions in the document, so a real page ID gave the wrong page or an error (`-ID 0` failed even though the first page of a new document has ID 0). In releases after 4.7.3 `-ID` is a real page ID lookup, as this page always described, and `-Index` is the way to ask for a position. If a script used `-ID 2` to mean "the second page", change it to `-Index 2` ([#232](https://github.com/saveenr/VisioAutomation/issues/232)).

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
