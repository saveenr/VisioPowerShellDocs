# Join-VisioShape

The **Join-VisioShape** cmdlet groups two or more shapes into a single group shape. With no arguments it groups whatever is currently selected; pass `-Shape` to specify shapes explicitly. Returns the new group shape.

## Syntax

```powershell
Join-VisioShape [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Shape` | `Shape[]` | No | Shapes to group. If omitted, the active selection is grouped. |

## Examples

### Group the current selection

```powershell
# Select some shapes first
$g = Join-VisioShape
```

### Group specific shapes

```powershell
$g = Join-VisioShape -Shape $shape1,$shape2,$shape3
```

## See also

* [Split-VisioShape](ungroup.md) &mdash; the inverse: ungroup a group.
* [Examples of Join-VisioShape and Split-VisioShape](examples.md)
