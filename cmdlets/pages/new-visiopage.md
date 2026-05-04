# New-VisioPage

The **New-VisioPage** cmdlet adds a new page to a Visio document and returns it. With no arguments it creates a default-sized blank page in the active document; pass `-Width`/`-Height` to set page size, `-Name` to set the page name, `-Cells` to apply ShapeSheet cells (page-level), or `-Document` to add the page to a specific document.

## Syntax

```powershell
New-VisioPage [-Name <String>] [-Width <Double>] [-Height <Double>]
              [-Cells <PageCells>] [-Document <Document>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Name` | `String` | No | Name for the new page. Empty/whitespace-only names are rejected. |
| `-Width` | `Double` | No | Page width in inches. Ignored when omitted. |
| `-Height` | `Double` | No | Page height in inches. Ignored when omitted. |
| `-Cells` | `PageCells` | No | A `PageCells` object (from [`New-VisioPageCells`](new-visiopagecells.md)) applied to the new page's PageSheet. If `-Width`/`-Height` are also given they override the corresponding cells. |
| `-Document` | `Document` | No | The document to add the page to. If omitted, the active document is used. |

## Examples

### Create a default-sized page in the active document

```powershell
$page = New-VisioPage
```

### Create a page with a specific size and name

```powershell
$page = New-VisioPage -Width 10.0 -Height 4.0 -Name "MyPage1"
```

### Create a page with a fully populated PageCells

```powershell
$cells = New-VisioPageCells
$cells.PageWidth  = 11
$cells.PageHeight = 8.5
# ... set any other PageSheet cells you care about

$page = New-VisioPage -Name "Letter" -Cells $cells
```

## See also

* [Get-VisioPage](get-visiopage.md)
* [Remove-VisioPage](remove-visiopage.md)
* [Format-VisioPage](format-visiopage.md)
* [New-VisioPageCells](new-visiopagecells.md), [Set-VisioPageCells](set-visiopagecells.md)
