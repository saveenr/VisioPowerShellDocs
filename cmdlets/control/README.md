# Control

These cmdlets work with **control handles** &mdash; the yellow draggable diamonds attached to a shape that let a user adjust geometry interactively. Each handle is a row in the `Controls` section of the shape's ShapeSheet, with cells for position (`X`, `Y`), behavior (`XBehavior`, `YBehavior`, `XDynamics`, `YDynamics`), glue (`CanGlue`), and a tooltip (`Tip`).

* [`Get-VisioControl`](get-visiocontrol.md) &mdash; read existing control handles off one or more shapes.
* [`New-VisioControl`](new-visiocontrol.md) &mdash; add a new control handle to one or more shapes.
* [`Remove-VisioControl`](remove-visiocontrol.md) &mdash; delete a control handle by index.

A shape can have any number of control handles. Indices start at `0`.
