# Export-VisioShape

The **Export-VisioShape** cmdlet exports the active selection (or the shapes you pass via `-Shape`) to a file. The output format is inferred from the filename extension: `.html`, `.htm`, and `.xhtml` produce an HTML rendering; any other extension is treated as an image format and routed through Visio's native image-export.

## Syntax

```powershell
Export-VisioShape [-Filename] <String> [-Overwrite] [-Shape <Shape[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Filename` | `String` | Yes (positional) | Output path. Format inferred from the extension. |
| `-Overwrite` | `SwitchParameter` | No | Allow overwriting an existing file. Without this switch the cmdlet refuses to clobber. |
| `-Shape` | `Shape[]` | No | Shapes to export. If omitted, the active selection is used. When supplied, those shapes are first selected, then exported. |

## Examples

### Export the current selection to a PNG

```powershell
Export-VisioShape -Filename "selection.png"
```

### Overwrite an existing file

```powershell
Export-VisioShape -Filename "selection.png" -Overwrite
```

### Export specific shapes

```powershell
$shapes = Get-VisioShape
Export-VisioShape -Filename "two-shapes.svg" -Shape $shapes[0],$shapes[1]
```

### Export to HTML

```powershell
Export-VisioShape -Filename "selection.html"
```

## See also

* [Export-VisioPage](../pages/export-visiopage.md) &mdash; the whole-page counterpart.
* [Select-VisioShape](selecting-shapes.md) &mdash; control what's selected before exporting.
