# Remove-VisioShape

The `Remove-VisioShape` cmdlet deletes shapes from the active page.

### Delete the current selection

With no arguments, the cmdlet deletes whatever shapes are currently selected.

```powershell
Remove-VisioShape
```

### Delete specific shapes

Pass an `IVisio.Shape` or an array of shapes via `-Shape`.

```powershell
$shapes = Get-VisioShape

# delete the first shape
Remove-VisioShape -Shape $shapes[0]

# delete the first and third shapes
Remove-VisioShape -Shape $shapes[0],$shapes[2]
```

### Delete all shapes on the page

```powershell
Select-VisioShape All
Remove-VisioShape
```

### See also

* [New-VisioShape](new-visioshape.md)
* [Select-VisioShape](selecting-shapes.md)
