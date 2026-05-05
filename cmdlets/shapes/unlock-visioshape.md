# Unlock-VisioShape

The **Unlock-VisioShape** cmdlet clears lock cells on a shape's ShapeSheet. Each switch corresponds to a `Lock*` cell; pass the switches for the locks you want to disable. Locks not mentioned in the call are left unchanged.

When `-Shape` is omitted, the cmdlet operates on the active selection.

> **Requires Visio PowerShell 4.6.1 or later.** Earlier versions had a binder bug that silently ignored these switches.

## Syntax

```powershell
Unlock-VisioShape [-Aspect] [-Begin] [-CalcWH] [-Crop] [-CustProp] [-Delete]
                  [-End] [-Format] [-FromGroupFormat] [-Group] [-Height]
                  [-MoveX] [-MoveY] [-Rotate] [-Select] [-TextEdit]
                  [-ThemeColors] [-ThemeEffects] [-VertexEdit] [-Width]
                  [-Shape <Shape[]>]
```

## Parameters

The available switches mirror those of [Lock-VisioShape](lock-visioshape.md); see that page for the per-switch effect description. Each is `SwitchParameter` and optional. The non-switch parameter:

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Shape` | `Shape[]` | No | Shapes to unlock. If omitted, the active selection is used. |

## Examples

### Re-allow movement on the current selection

```powershell
Unlock-VisioShape -MoveX -MoveY
```

### Unlock specific shapes

```powershell
$shapes = Get-VisioShape
Unlock-VisioShape -Delete -Format -Shape $shapes[0]
```

### Clear every lock

```powershell
Unlock-VisioShape -Aspect -Begin -CalcWH -Crop -CustProp -Delete `
                  -End -Format -FromGroupFormat -Group -Height `
                  -MoveX -MoveY -Rotate -Select -TextEdit `
                  -ThemeColors -ThemeEffects -VertexEdit -Width
```

## See also

* [Lock-VisioShape](lock-visioshape.md): full description of each switch.
* `Get-VisioLockCells` (covered in the [Other cmdlets](../other-cmdlets.md) note).
