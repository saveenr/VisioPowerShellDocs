# VisioApplication

The **VisioApplication** cmdlets manage the Visio application process itself &mdash; starting it, attaching to it, undoing/redoing actions, and rendering high-level diagram models into a real Visio drawing.

The PowerShell session binds to one Visio application at a time. Most cmdlets in the module need an attached application; if one isn't running, [`New-VisioApplication`](new-visioapplication.md) starts one.

### Lifecycle

* [`New-VisioApplication`](new-visioapplication.md) &mdash; start a new Visio application and bind to it.
* [`Get-VisioApplication`](get-visioapplication.md) &mdash; return the currently bound application object (or `$null`).
* [`Test-VisioApplication`](test-visioapplication.md) &mdash; boolean: is an application currently bound?
* [`Close-VisioApplication`](close-visioapplication.md) &mdash; shut down the bound application (without prompting for unsaved changes).

### Edit history

* [`Undo-VisioApplication`](undo-visioapplication.md) &mdash; undo the last action (Ctrl+Z equivalent).
* [`Redo-VisioApplication`](redo-visioapplication.md) &mdash; redo the last undone action.

### Diagram rendering

* [`Out-VisioApplication`](out-visioapplication.md) &mdash; render a model object (org chart, directed graph, grid, data table, XML) into the bound application as a real drawing. The endpoint of the [Automatic diagrams](../../automatic-diagrams/README.md) family.
