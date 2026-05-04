# ShapeCells

These cmdlets work with the ShapeSheet of shapes &mdash; size, position, fill, line, character formatting, and many other cells.

* [`New-VisioShapeCells`](new-visioshapecells.md) &mdash; create a blank `ShapeCells` object to populate.
* [`Get-VisioShapeCells`](get-visioshapecells.md) &mdash; read cells off one or more shapes as a DataTable.
* `Set-VisioShapeCells` &mdash; write a populated `ShapeCells` to one or more shapes (covered in [Shape cells](working-with-shape-cells.md) and [Set-VisioShapeCells for text](format-text.md)).

The pattern is the same for all of them: build a cells object, set the properties you care about, write it back.
