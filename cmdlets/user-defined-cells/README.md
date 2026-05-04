# User-defined cells

A shape's ShapeSheet has a **User-Defined Cells** section &mdash; a list of named cells you can use as your own variables in formulas elsewhere on the shape. Each entry has a `Value` formula and an optional `Prompt` (description). They behave like custom properties but are intended for the shape's internal logic rather than the UI.

* [`Get-VisioUserDefinedCell`](get-visiouserdefinedcell.md) &mdash; read the user-defined cells on one or more shapes.
* [`Set-VisioUserDefinedCell`](set-visiouserdefinedcell.md) &mdash; add or update a named cell.
* [`Remove-VisioUserDefinedCell`](remove-visiouserdefinedcell.md) &mdash; delete a named cell.

For UI-facing properties (Name / Value / Label / Prompt / Type / Format etc., shown in Visio's Shape Data window), see [Custom properties](../custom-properties/README.md) instead.
