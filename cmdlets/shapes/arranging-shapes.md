# Format-VisioShape

The **Format-VisioShape** cmdlet arranges the active selection: nudge by an offset, align edges/centers, or distribute evenly along an axis. The cmdlet operates on whatever is currently selected; use [Select-VisioShape](selecting-shapes.md) first if you need to set up the selection.

## Syntax

```powershell
Format-VisioShape [-NudgeX <Double>] [-NudgeY <Double>]
                  [-AlignHorizontal <AlignmentHorizontal>]
                  [-AlignVertical <AlignmentVertical>]
                  [-DistributeHorizontal] [-DistributeVertical]
                  [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-NudgeX` | `Double` | No | Horizontal move (inches). Positive = right, negative = left. |
| `-NudgeY` | `Double` | No | Vertical move (inches). Positive = up, negative = down. |
| `-AlignHorizontal` | `AlignmentHorizontal` | No | One of `Left`, `Center`, `Right`. |
| `-AlignVertical` | `AlignmentVertical` | No | One of `Top`, `Center`, `Bottom`. |
| `-DistributeHorizontal` | `SwitchParameter` | No | Space the selection evenly along the X axis. |
| `-DistributeVertical` | `SwitchParameter` | No | Space the selection evenly along the Y axis. |
| `-Shape` | `Shape[]` | No | Shapes to operate on. If omitted, the active selection is used. When supplied, those shapes are first selected, then formatted. |

## Examples

### Nudge

```powershell
# nudge shape 1 inch right
Format-VisioShape -NudgeX 1

# nudge shape 1 inch left
Format-VisioShape -NudgeX -1

# nudge shape 1 inch up
Format-VisioShape -NudgeY 1

# nudge shape 1 inch down
Format-VisioShape -NudgeY -1
```

### Align shapes

```powershell
# Align vertically
Format-VisioShape -AlignVertical Top
Format-VisioShape -AlignVertical Center
Format-VisioShape -AlignVertical Bottom

# Align horizontally
Format-VisioShape -AlignHorizontal Left
Format-VisioShape -AlignHorizontal Center
Format-VisioShape -AlignHorizontal Right

# Combine
Format-VisioShape -AlignHorizontal Left -AlignVertical Bottom
```

### Distribute shapes evenly

```powershell
# Evenly along the X axis
Format-VisioShape -DistributeHorizontal

# Evenly along the Y axis
Format-VisioShape -DistributeVertical
```

## See also

* [Select-VisioShape](selecting-shapes.md): control what's selected before formatting.
* [Format-VisioPage](../pages/format-visiopage.md): page-level layout / sizing.
