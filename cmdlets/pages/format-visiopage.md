# Format-VisioPage

The **Format-VisioPage** cmdlet changes page-level layout and presentation: page size, orientation, fit-to-contents, background-page assignment, and automatic shape layout. Multiple options can be combined in a single call.

When `-Page` is omitted the cmdlet operates on the active page.

## Syntax

```powershell
Format-VisioPage [-Width <Double>] [-Height <Double>]
                 [-FitContents] [-BorderWidth <Double>] [-BorderHeight <Double>]
                 [-Orientation <PageOrientation>]
                 [-BackgroundPage <String>]
                 [-LayoutStyle <LayoutStyleBase>]
                 [-Page <Page[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Width` | `Double` | No | New page width (inches). Ignored when omitted. |
| `-Height` | `Double` | No | New page height (inches). Ignored when omitted. |
| `-FitContents` | `SwitchParameter` | No | Resize the page to fit its current contents. Combine with `-BorderWidth`/`-BorderHeight` for padding. |
| `-BorderWidth` | `Double` | No | Horizontal padding when using `-FitContents`. |
| `-BorderHeight` | `Double` | No | Vertical padding when using `-FitContents`. |
| `-Orientation` | `PageOrientation` | No | `Portrait` or `Landscape`. |
| `-BackgroundPage` | `String` | No | Name of an existing page to assign as the background. |
| `-LayoutStyle` | `LayoutStyleBase` | No | A layout-style instance (`FlowchartLayoutStyle`, `RadialLayoutStyle`, etc.) used to auto-arrange shapes. |
| `-Page` | `Page[]` | No | Page(s) to format. If omitted, the active page is used. |

## Examples

### Change the page size

```powershell
Format-VisioPage -Width 10.0 -Height 4.0
```

### Resize the page to fit its contents

```powershell
Format-VisioPage -FitContents
```

With extra padding:

```powershell
Format-VisioPage -FitContents -BorderWidth 1.0 -BorderHeight 1.0
```

### Set page orientation

```powershell
Format-VisioPage -Orientation Portrait
Format-VisioPage -Orientation Landscape
```

### Assign a background page

```powershell
Format-VisioPage -BackgroundPage "BG-Layout"
```

### Auto-layout shapes

Visio's layout engine can re-arrange the shapes on a page using one of the layout-style classes from `VisioAutomation.Models.LayoutStyles`. Construct the style, set the parameters you want, and pass it to `-LayoutStyle`. `Import-Module Visio` already loads the VisioAutomation assemblies, so the types are reachable via `New-Object` directly; no extra `Add-Type` call is needed.

```powershell
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

New-VisioDocument

$shape_a = New-VisioShape -Rectangle (New-VisioRectangle 5 7 6 8)
Set-VisioText "A" -Shape $shape_a
$shape_b = New-VisioShape -Rectangle (New-VisioRectangle 3 5 4 6)
Set-VisioText "B" -Shape $shape_b
$shape_c = New-VisioShape -Rectangle (New-VisioRectangle 7 5 8 6)
Set-VisioText "C" -Shape $shape_c

Connect-VisioShape -From $shape_a -To $shape_b
Connect-VisioShape -From $shape_a -To $shape_c

$ls = New-Object VisioAutomation.Models.LayoutStyles.FlowchartLayoutStyle
$ls.AvenueSizeX = 1
$ls.AvenueSizeY = 0.5

Format-VisioPage -LayoutStyle $ls
```

## See also

* [Get-VisioPage](get-visiopage.md)
* [New-VisioPage](new-visiopage.md)
* [Measure-VisioPage](measure-visiopage.md)
