# Shapes

The **shape** cmdlets are the largest section of the module. They cover everything you can do with the actual content of a Visio drawing &mdash; creating shapes, deleting them, selecting them, connecting them with lines, grouping and ungrouping, exporting, and locking down their behavior.

### Create / delete

* [`New-VisioShape`](new-visioshape.md) &mdash; the central cmdlet. Drops a master onto the page, or draws a primitive (rectangle, oval, line, polyline, Bezier).
* [`Remove-VisioShape`](remove-visioshape.md) &mdash; delete shapes.
* [`Copy-VisioShape`](copy-visioshape.md) &mdash; duplicate shapes (preserves all formatting).

### Selection

Visio's *active selection* is what most cmdlets target by default.

* [`Get-VisioShape`](enumerate-selected-shapes.md) &mdash; read the current selection, or look up shapes by name / ID.
* [`Select-VisioShape`](selecting-shapes.md) &mdash; change the active selection. Pass shapes explicitly, or one of the high-level operations: [SelectAll, SelectNone](clearing-the-selection.md), [InvertSelection](invert-the-selection.md).
* [`Test-VisioShape`](test-visioshape.md) &mdash; boolean: is anything currently selected?

### Connecting

* [`Connect-VisioShape`](connect-shapes.md) &mdash; draw connectors between shapes.

### Grouping

* [`Join-VisioShape`](create-groups.md) &mdash; combine shapes into a group.
* [`Split-VisioShape`](ungroup.md) &mdash; ungroup a group back into its members.
* [Examples of Join-VisioShape and Split-VisioShape](examples.md)

### Layout / arrangement

* [`Format-VisioShape`](arranging-shapes.md) &mdash; nudge, align, distribute the active selection.

### Export

* [`Export-VisioShape`](export-visioshape.md) &mdash; export the selection to an image or HTML file.

### Locking

Locks live as cells in the shape's ShapeSheet (`LockMoveX`, `LockDelete`, `LockTextEdit`, ...).

* [`Lock-VisioShape`](lock-visioshape.md) &mdash; enable specific lock cells (1).
* [`Unlock-VisioShape`](unlock-visioshape.md) &mdash; clear specific lock cells (0).

### Related

* [ShapeCells](../shapecells/README.md) &mdash; reading and writing arbitrary ShapeSheet cells.
* [Custom properties](../custom-properties/README.md) &mdash; shape-data attached to a shape.
* [User-defined cells](../user-defined-cells/README.md) &mdash; named values used as variables in formulas.
