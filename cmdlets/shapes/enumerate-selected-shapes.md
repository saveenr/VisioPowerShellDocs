# Get-VisioShape

The **Get-VisioShape** cmdlet returns shapes from the active page. With no arguments it returns the **currently selected** shapes. Other parameter sets return shapes by name (no wildcards) or by Visio shape ID. Use `-Page` to read from a specific page rather than the active one.

## Syntax

```powershell
# The current selection (default)
Get-VisioShape [-Page <Page>]

# All shapes on a page, or by name
Get-VisioShape [-Name <String[]>] [-Page <Page>]

# By Visio shape ID
Get-VisioShape [-ID <Int32[]>] [-Page <Page>]

# Just the active selection (explicit)
Get-VisioShape [-ActiveSelection] [-Page <Page>]
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-Name` | `String[]` | No | shapebyname | One or more shape names. Wildcards are **not** supported &mdash; names must match exactly. |
| `-ID` | `Int32[]` | No | shapebyid | One or more numeric Visio shape IDs. |
| `-ActiveSelection` | `SwitchParameter` | No | active | Return the active selection. Same behavior as the no-argument default. |
| `-Page` | `Page` | No | All | Page to read from. If omitted, the active page is used. |

## Examples

### Get the currently selected shapes

```powershell
$shapes = Get-VisioShape
```

### Get every shape on the active page

When you want all shapes regardless of selection, omit `-ActiveSelection` and don't pass `-Name` or `-ID`.

```powershell
$shapes = Get-VisioShape -ActiveSelection:$false
# or simply call with no arguments after Select-VisioShape SelectAll:
Select-VisioShape SelectAll
$shapes = Get-VisioShape
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
