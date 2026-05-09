# Control

These cmdlets work with **control handles**: the yellow draggable diamonds attached to a shape that let a user adjust geometry interactively. Each handle is a row in the `Controls` section of the shape's ShapeSheet, with cells for position (`X`, `Y`), behavior (`XBehavior`, `YBehavior`, `XDynamics`, `YDynamics`), glue (`CanGlue`), and a tooltip (`Tip`).

* [`Get-VisioControl`](get-visiocontrol.md): read existing control handles off one or more shapes.
* [`New-VisioControl`](new-visiocontrol.md): add a new control handle to one or more shapes.
* [`Remove-VisioControl`](remove-visiocontrol.md): delete a control handle by index.

A shape can have any number of control handles. Indices start at `0`.

## On the C# side

These cmdlets wrap the [`client.Control`](https://saveenr.gitbook.io/visioautomation/visio-scripting/control) command group on the VisioAutomation gitbook. See [VisioScripting.Client](https://saveenr.gitbook.io/visioautomation/visio-scripting) for the full facade index.
