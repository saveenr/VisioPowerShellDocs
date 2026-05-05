# Format-VisioWindow

The **Format-VisioWindow** cmdlet controls the active window's zoom level and (optionally) its on-screen rectangle.

The cmdlet has three mutually-exclusive zoom forms: `-ZoomTo` for high-level zoom-to-fit operations, `-Zoom` for an absolute zoom factor, and `-ZoomRelative` for an incremental change. The window-rectangle parameters (`-Width`, `-Height`, `-X`, `-Y`) can be combined with any of those.

## Syntax

```powershell
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
| `-Width` | `Int32` | No | All | Window width in pixels. |
| `-Height` | `Int32` | No | All | Window height in pixels. |
| `-X` | `Int32` | No | All | Window left in pixels. |
| `-Y` | `Int32` | No | All | Window top in pixels. |

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
Format-VisioWindow -Width 1600 -Height 900 -X 100 -Y 50 -ZoomTo Page
```
