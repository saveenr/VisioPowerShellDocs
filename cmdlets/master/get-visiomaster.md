# Get-VisioMaster

The **Get-VisioMaster** cmdlet returns one or more masters (stencil shapes) from a Visio document. With no arguments it returns every master in the active document. Pass `-Name` to filter by master name (or pass an array for multiple), and `-Document` to read from a specific document instead of the active one.

## Syntax

```powershell
Get-VisioMaster [[-Name] <String[]>] [-Document <Document>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Name` | `String[]` | No (positional) | One or more master names. If omitted, all masters in the document are returned. |
| `-Document` | `Document` | No | Document (typically a stencil) to search. If omitted, the active document is used. |

## Examples

### Get every master in the active document

```powershell
Get-VisioMaster
```

### Get masters from a specific document

```powershell
Get-VisioMaster -Document $doc
```

### Get a master by name from the active document

```powershell
Get-VisioMaster -Name "Rectangle"
```

Or positionally:

```powershell
Get-VisioMaster "Rectangle"
```

### Get a master from a specific stencil

```powershell
$basic_u = Open-VisioDocument "basic_u.vss"
$rect_m  = Get-VisioMaster -Name "Rectangle" -Document $basic_u
```

### End-to-end: open a stencil, get a master, drop and label it

```powershell
Import-Module Visio

New-VisioApplication
New-VisioDocument

$basic_u = Open-VisioDocument "basic_u.vss"
$master  = Get-VisioMaster -Name "Rectangle" -Document $basic_u
$shape   = New-VisioShape -Master $master -Position (New-VisioPoint 4 5)

Set-VisioText "Hello World" -Shape $shape
```

## See also

* [Open-VisioDocument](../documents/open-visiodocument.md): open a stencil so you can read its masters.
* [New-VisioShape](../shapes/new-visioshape.md): drop a master onto a page.
