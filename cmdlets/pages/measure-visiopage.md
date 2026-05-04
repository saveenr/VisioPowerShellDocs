# Measure-VisioPage

The **Measure-VisioPage** cmdlet returns dimension records for one or more pages &mdash; width, height, margins, and other layout-relevant numbers. The output is a list of `PageDimensions` objects, one per page.

When `-Page` is omitted, the cmdlet measures the active page.

## Syntax

```powershell
Measure-VisioPage [-Page <Page[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Page` | `Page[]` | No | The page(s) to measure. If omitted, the active page is used. |

## Examples

### Measure the active page

```powershell
$dim = Measure-VisioPage
$dim | Format-List
```

### Measure specific pages

```powershell
$pages = Get-VisioPage
Measure-VisioPage -Page $pages[0],$pages[2]
```

### Measure every page in the document

```powershell
$dims = Measure-VisioPage -Page (Get-VisioPage)
$dims | Format-Table
```

## See also

* [Get-VisioPage](get-visiopage.md)
* [Format-VisioPage](format-visiopage.md)
* `Measure-VisioShape` &mdash; the shape-level counterpart (covered in the [Other cmdlets](../other-cmdlets.md) note).
