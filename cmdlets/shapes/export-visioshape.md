# Export-VisioShape

The `Export-VisioShape` cmdlet exports the active selection (or the shapes you pass via `-Shape`) to a file. The output format is inferred from the filename extension: `.html`, `.htm`, and `.xhtml` produce an HTML rendering; any other extension is treated as an image format and routed through Visio's native image-export.

`-Filename` is required and positional.

### Export the current selection to a PNG

```powershell
Export-VisioShape -Filename "selection.png"
```

### Overwrite an existing file

If the target file already exists, the cmdlet refuses to overwrite it unless you pass `-Overwrite`.

```powershell
Export-VisioShape -Filename "selection.png" -Overwrite
```

### Export specific shapes

When `-Shape` is supplied, the cmdlet first selects those shapes, then exports the selection.

```powershell
$shapes = Get-VisioShape
Export-VisioShape -Filename "two-shapes.svg" -Shape $shapes[0],$shapes[1]
```

### Export to HTML

```powershell
Export-VisioShape -Filename "selection.html"
```

### See also

* [Export-VisioPage](../pages/export-visiopage.md) &mdash; the whole-page counterpart.
* [Select-VisioShape](selecting-shapes.md) &mdash; control what's selected before exporting.
