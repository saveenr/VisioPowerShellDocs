# Get-VisioShapeCells

The `Get-VisioShapeCells` cmdlet reads ShapeSheet cells from one or more shapes and returns the result as a `System.Data.DataTable`. The table has one row per shape and an extra `ShapeID` column to disambiguate them.

### Read all known cells from the current selection

When `-Shape` is omitted, the cmdlet reads the active selection.

```powershell
$dt = Get-VisioShapeCells
Write-Host $dt
```

### Read specific shapes

```powershell
$shapes = Get-VisioShape
$dt = Get-VisioShapeCells -Shape $shapes[0],$shapes[2]
```

### Read specific cells only

`-Cell` accepts one or more cell names and supports wildcards.

```powershell
# only fill-related cells
$dt = Get-VisioShapeCells -Cell "FillForeground","FillBackground","FillPattern"

# wildcard
$dt = Get-VisioShapeCells -Cell "Char*"
```

### Read result values instead of formulas

By default, the DataTable holds the cell **formulas**. Use `-Results` to get the resolved values. `-ResultType` chooses the .NET type used in the table: `String` (default), `Double`, `Int`, or `Bool`.

```powershell
# resolved values, formatted as strings (the default)
$dt = Get-VisioShapeCells -Results

# resolved values, returned as Double where applicable
$dt = Get-VisioShapeCells -Results -ResultType Double
```

### See also

* [New-VisioShapeCells](new-visioshapecells.md)
* [Shape cells](working-with-shape-cells.md)
