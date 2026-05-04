# Custom properties

Visio's **custom properties** (also known as *shape data*) are user-facing key/value fields you can attach to a shape. They appear in Visio's Shape Data window and are commonly used to record metadata: server name, owner, cost, region, due date, and so on. Each property has a `Value` plus optional metadata: `Label`, `Prompt`, `Type`, `Format`, `LangID`, `SortKey`, `Calendar`, `Ask`, `Invisible`.

* [`Get-VisioCustomProperty`](get-visiocustomproperty.md) &mdash; read the custom properties on one or more shapes.
* [`Set-VisioCustomProperty`](set-visiocustomproperty.md) &mdash; add or update a custom property by name (or pass a populated `CustomPropertyCells` for fine-grained control).
* [`Remove-VisioCustomProperty`](remove-visiocustomproperty.md) &mdash; delete a custom property by name.
* [Examples](examples.md) &mdash; an end-to-end walkthrough.

For internal-use named values (used as variables in shape formulas, not surfaced in the UI), see [User-defined cells](../user-defined-cells/README.md) instead.
