# Lock-VisioShape

The **Lock-VisioShape** cmdlet sets one or more lock cells on a shape's ShapeSheet. Each switch corresponds to a `Lock*` cell; pass the switches for the locks you want to enable. Locks not mentioned in the call are left unchanged. Pair with [Unlock-VisioShape](unlock-visioshape.md) to clear locks.

When `-Shape` is omitted, the cmdlet operates on the active selection.

> **Requires Visio PowerShell 4.6.1 or later.** Earlier versions had a binder bug that silently ignored these switches.

## Syntax

```powershell
Lock-VisioShape [-Aspect] [-Begin] [-CalcWH] [-Crop] [-CustProp] [-Delete]
                [-End] [-Format] [-FromGroupFormat] [-Group] [-Height]
                [-MoveX] [-MoveY] [-Rotate] [-Select] [-TextEdit]
                [-ThemeColors] [-ThemeEffects] [-VertexEdit] [-Width]
                [-Shape <Shape[]>]
```

## Parameters

| Parameter | ShapeSheet cell | Effect |
| --- | --- | --- |
| `-Aspect` | `LockAspect` | Preserves width-to-height ratio when sized. |
| `-Begin` | `LockBegin` | Begin endpoint cannot be moved. |
| `-CalcWH` | `LockCalcWH` | Width / height formulas can't be recalculated. |
| `-Crop` | `LockCrop` | Cropping is disabled. |
| `-CustProp` | `LockCustProp` | Custom (shape-data) properties cannot be edited. |
| `-Delete` | `LockDelete` | Shape cannot be deleted. |
| `-End` | `LockEnd` | End endpoint cannot be moved. |
| `-Format` | `LockFormat` | Formatting is locked. |
| `-FromGroupFormat` | `LockFromGroupFormat` | Group formatting cannot reach the shape. |
| `-Group` | `LockGroup` | Cannot be grouped or ungrouped. |
| `-Height` | `LockHeight` | Height cannot be changed. |
| `-MoveX` | `LockMoveX` | Cannot be moved horizontally. |
| `-MoveY` | `LockMoveY` | Cannot be moved vertically. |
| `-Rotate` | `LockRotate` | Cannot be rotated. |
| `-Select` | `LockSelect` | Cannot be selected. |
| `-TextEdit` | `LockTextEdit` | Text cannot be edited. |
| `-ThemeColors` | `LockThemeColors` | Theme color changes don't apply. |
| `-ThemeEffects` | `LockThemeEffects` | Theme effect changes don't apply. |
| `-VertexEdit` | `LockVertexEdit` | Geometry vertices cannot be edited. |
| `-Width` | `LockWidth` | Width cannot be changed. |
| `-Shape` | (target) | Shapes to lock. If omitted, the active selection is used. |

All lock switches are `SwitchParameter` and optional.

## Examples

### Lock the current selection so it can't be moved or resized

```powershell
Lock-VisioShape -MoveX -MoveY -Width -Height
```

### Lock specific shapes

```powershell
$shapes = Get-VisioShape
Lock-VisioShape -Delete -Shape $shapes[0],$shapes[2]
```

### Inspect lock state

```powershell
$dict = Get-VisioLockCells
$shape = $dict.Keys | Select-Object -First 1
$dict[$shape]
```

## See also

* [Unlock-VisioShape](unlock-visioshape.md)
* `Get-VisioLockCells` (covered in the [Other cmdlets](../other-cmdlets.md) note).
