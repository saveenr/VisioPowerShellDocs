# Get-VisioShape

The **Get-VisioShape** cmdlet returns shapes from the active page. With no arguments it returns **every shape** on the page; pass `-ActiveSelection` for just the currently-selected shapes, `-Name` to filter by exact name, or `-ID` to look up shapes by their numeric Visio ID. Use `-Page` to read from a specific page rather than the active one.

## Syntax

```powershell
# Every shape on the page (default), or filter by exact name
Get-VisioShape [-Name <String[]>] [-Page <Page>]

# By Visio shape ID
Get-VisioShape [-ID <Int32[]>] [-Page <Page>]

# Just the active selection
Get-VisioShape [-ActiveSelection] [-Page <Page>]
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-Name` | `String[]` | No | shapebyname | One or more shape names. Wildcards are **not** supported &mdash; names must match exactly. |
| `-ID` | `Int32[]` | No | shapebyid | One or more numeric Visio shape IDs. |
| `-ActiveSelection` | `SwitchParameter` | No | active | Return only the currently-selected shapes on the page. |
| `-Page` | `Page` | No | All | Page to read from. If omitted, the active page is used. |

## Examples

### Get every shape on the active page

```powershell
$shapes = Get-VisioShape
```

### Get just the currently-selected shapes

```powershell
$selected = Get-VisioShape -ActiveSelection
```

### Get a specific shape by name

```powershell
$shapes = Get-VisioShape -Name "Sheet.5"
```

### Get shapes by ID

```powershell
$shapes = Get-VisioShape -ID 1,3,7
```

### Get shapes from a specific page

```powershell
$page = Get-VisioPage "Settings"
$shapes = Get-VisioShape -Page $page
```

## See also

* [Select-VisioShape](selecting-shapes.md) &mdash; change the selection.
* [Test-VisioShape](test-visioshape.md) &mdash; check whether anything is selected.
* [New-VisioShape](new-visioshape.md), [Remove-VisioShape](remove-visioshape.md)
