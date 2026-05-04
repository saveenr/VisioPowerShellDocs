# Copy-VisioShape

The `Copy-VisioShape` cmdlet duplicates one or more shapes on the active page. It uses Visio's native duplicate operation, so the new shapes inherit all formatting and ShapeSheet values from the originals. After the cmdlet runs, the duplicated shapes become the active selection.

The cmdlet does not return the new shapes &mdash; use [`Get-VisioShape`](selecting-shapes.md) afterward if you need handles to them.

### Duplicate the current selection

With no arguments, the cmdlet duplicates whatever shapes are currently selected.

```powershell
Copy-VisioShape
```

### Duplicate specific shapes

When `-Shape` is supplied, the cmdlet first selects those shapes, then duplicates the selection.

```powershell
$shapes = Get-VisioShape

# duplicate one shape
Copy-VisioShape -Shape $shapes[0]

# duplicate several
Copy-VisioShape -Shape $shapes[0],$shapes[2]
```

### Capture the duplicated shapes

Because the duplicates become the new selection, you can grab them right after with `Get-VisioShape`.

```powershell
Copy-VisioShape -Shape $shapes[0]
$copies = Get-VisioShape
```

### See also

* [New-VisioShape](new-visioshape.md)
* [Remove-VisioShape](remove-visioshape.md)
* [Select-VisioShape](selecting-shapes.md)
