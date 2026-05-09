# Shapes

The **shape** cmdlets are the largest section of the module. They cover everything you can do with the actual content of a Visio drawing: creating shapes, deleting them, selecting them, connecting them with lines, grouping and ungrouping, exporting, and locking down their behavior.

### Create / delete

* [`New-VisioShape`](new-visioshape.md): the central cmdlet. Drops a master onto the page, or draws a primitive (rectangle, oval, line, polyline, Bezier).
* [`Remove-VisioShape`](remove-visioshape.md): delete shapes.
* [`Copy-VisioShape`](copy-visioshape.md): duplicate shapes (preserves all formatting).

### Selection

Visio's *active selection* is what most cmdlets target by default.

* [`Get-VisioShape`](enumerate-selected-shapes.md): read the current selection, or look up shapes by name / ID.
* [`Select-VisioShape`](selecting-shapes.md): change the active selection. Pass shapes explicitly, or one of the high-level operations: [SelectAll, SelectNone](clearing-the-selection.md), [InvertSelection](invert-the-selection.md).
* [`Test-VisioShape`](test-visioshape.md): boolean: is anything currently selected?

### Connecting

* [`Connect-VisioShape`](connect-shapes.md): draw connectors between shapes.

### Grouping

* [`Join-VisioShape`](create-groups.md): combine shapes into a group.
* [`Split-VisioShape`](ungroup.md): ungroup a group back into its members.
* [Examples of Join-VisioShape and Split-VisioShape](examples.md)

### Layout / arrangement

* [`Format-VisioShape`](arranging-shapes.md): nudge, align, distribute the active selection.

### Export

* [`Export-VisioShape`](export-visioshape.md): export the selection to an image or HTML file.

### Locking

Locks live as cells in the shape's ShapeSheet (`LockMoveX`, `LockDelete`, `LockTextEdit`, ...).

* [`Lock-VisioShape`](lock-visioshape.md): enable specific lock cells (1).
* [`Unlock-VisioShape`](unlock-visioshape.md): clear specific lock cells (0).

## On the C# side

Shape-level operations on the C# side are spread across several command groups on the VisioAutomation gitbook: [`client.Selection`](https://saveenr.gitbook.io/visioautomation/visio-scripting/selection) (current-selection operations), [`client.Draw`](https://saveenr.gitbook.io/visioautomation/visio-scripting/draw) (draw primitives), [`client.Arrange`](https://saveenr.gitbook.io/visioautomation/visio-scripting/arrange) (align, distribute, nudge), [`client.Grouping`](https://saveenr.gitbook.io/visioautomation/visio-scripting/grouping) (group / ungroup), [`client.Lock`](https://saveenr.gitbook.io/visioautomation/visio-scripting/lock) (lock cells), [`client.Hyperlink`](https://saveenr.gitbook.io/visioautomation/visio-scripting/hyperlink), and [`client.Connection`](https://saveenr.gitbook.io/visioautomation/visio-scripting/connection). See [VisioScripting.Client](https://saveenr.gitbook.io/visioautomation/visio-scripting) for the full facade index.

### Related

* [ShapeCells](../shapecells/README.md): reading and writing arbitrary ShapeSheet cells.
* [Custom properties](../custom-properties/README.md): shape-data attached to a shape.
* [User-defined cells](../user-defined-cells/README.md): named values used as variables in formulas.
