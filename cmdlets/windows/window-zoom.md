# Format-VisioWindow

The **Format-VisioWindow** cmdlet controls the active window's zoom level and its on-screen rectangle. You can set either one or both.

The cmdlet has four forms. The default form sets only the window rectangle (`-Width`, `-Height`, `-X`, `-Y`) and leaves the zoom alone. The other three are mutually exclusive zoom forms: `-ZoomTo` for high-level zoom-to-fit operations, `-Zoom` for an absolute zoom factor, and `-ZoomRelative` for an incremental change. Each zoom form can also set the rectangle.

> **Unreleased:** added after module 5.1.0 ([#290](https://github.com/saveenr/VisioAutomation/issues/290)). The rectangle-only form, `-X` and `-Y` on their own, and `-Width`, `-Height`, `-X` and `-Y` by position after the zoom parameter. In module 5.1.0 and earlier, every form required a zoom parameter, so `Format-VisioWindow -Width 900 -Height 700` failed with "Parameter set cannot be resolved", and `-Width` was missing from `Get-Command Format-VisioWindow -Syntax`. A zoom parameter combined with the rectangle by name (`-Zoom 1.5 -Width 900`) worked in every version.

## Syntax

```powershell
# Set only the window rectangle; the zoom is not changed (the default form)
Format-VisioWindow [-Width <Int32>] [-Height <Int32>] [-X <Int32>] [-Y <Int32>]

# Zoom to a target (page, selection, etc.)
Format-VisioWindow [-ZoomTo] <ZoomToObject>
                   [[-Width] <Int32>] [[-Height] <Int32>] [[-X] <Int32>] [[-Y] <Int32>]

# Set an absolute zoom factor (1.0 = 100%)
Format-VisioWindow [-Zoom] <Double>
                   [[-Width] <Int32>] [[-Height] <Int32>] [[-X] <Int32>] [[-Y] <Int32>]

# Multiply the current zoom by a relative factor
Format-VisioWindow [-ZoomRelative] <Double>
                   [[-Width] <Int32>] [[-Height] <Int32>] [[-X] <Int32>] [[-Y] <Int32>]
```

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-ZoomTo` | `ZoomToObject` | Yes (positional 0) | zoomto | One of `Page`, `PageWidth`, `Selection`. Auto-fits the view. |
| `-Zoom` | `Double` | Yes (positional 0) | value | Absolute zoom factor. `1.0` = 100%, `2.0` = 200%, `0.5` = 50%. |
| `-ZoomRelative` | `Double` | Yes (positional 0) | valuerelative | Multiplies the current zoom. `1.1` = +10%, `0.9` = -10%. |
| `-Width` | `Int32` | No | rect (default), zoomto, value, valuerelative | Window width in pixels. |
| `-Height` | `Int32` | No | rect (default), zoomto, value, valuerelative | Window height in pixels. |
| `-X` | `Int32` | No | rect (default), zoomto, value, valuerelative | Window left in pixels. |
| `-Y` | `Int32` | No | rect (default), zoomto, value, valuerelative | Window top in pixels. |

The rectangle parameters are named-only in the rectangle-only form. In the zoom forms they follow the zoom parameter by position (`-Width` is position 1, `-Height` 2, `-X` 3, `-Y` 4), so `Format-VisioWindow Page 700 500` zooms to the page and sets the width and height. A bare number is never taken as a window size: `Format-VisioWindow 900 700` is an error. Giving any of the four rectangle values moves or resizes the window; the ones you leave out keep their current value.

## Examples

### Zoom to a target

```powershell
Format-VisioWindow -ZoomTo Page
Format-VisioWindow -ZoomTo PageWidth
Format-VisioWindow -ZoomTo Selection
```

### Set an absolute zoom level

```powershell
Format-VisioWindow -Zoom 2.0   # 200%
Format-VisioWindow -Zoom 1.0   # 100%
Format-VisioWindow -Zoom 0.5   # 50%
Format-VisioWindow -Zoom 0.25  # 25%
```

### Zoom relative to the current value

```powershell
Format-VisioWindow -ZoomRelative 1.1   # zoom in 10%
Format-VisioWindow -ZoomRelative 0.9   # zoom out 10%
```

### Resize and reposition the Visio window

```powershell
# Rectangle only; the zoom is unchanged
Format-VisioWindow -Width 1600 -Height 900 -X 100 -Y 50

# Move the window without resizing it
Format-VisioWindow -X 0 -Y 0

# Rectangle and zoom together
Format-VisioWindow -Width 1600 -Height 900 -X 100 -Y 50 -ZoomTo Page
Format-VisioWindow -ZoomTo Page 1600 900
```
