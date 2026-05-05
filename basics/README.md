# Basics

If you're new to the Visio PowerShell module, start here. The basics section covers concepts and recipes that show up across nearly every script: how shapes get onto a page, how to find them again, how cells and formatting work, and how to discover what cmdlets are available.

## Concepts

* [Geometry primitives](geometry-primitves.md): the `Point`, `Rectangle`, and related types that geometry-taking cmdlets expect.
* [Context-sensitivity](context-sensitivity.md): how cmdlets default to "the active document / page / selection" when targets are omitted.

## Working with shapes

* [Drop shape masters](drop-masters.md): the recommended way to add shapes to a page.
* [Draw basic shapes](draw-basic-shapes.md): rectangle / oval / line / polyline / Bezier without a master.
* [Format shapes with cells](format-shapes-with-cells.md): setting size, color, line, fill via `ShapeCells`.
* [Enumerate shapes](enumerate-shapes.md): finding shapes already on a page.

## Working with pages

* [Create pages](create-pages.md): basic page creation.

## Application lifecycle

* [Bound Visio application](bound-visio-application.md): how the PowerShell session attaches to a Visio process.
* [Close Visio applications](close-visio-applications.md): tearing down cleanly.

## Discovering cmdlets

* [List cmdlets](list-cmdlets.md): using `Get-Command -Module Visio` to inspect the module's surface.
* [List of all cmdlets](list-of-all-cmdlets.md): static reference list.
* [Get help for a cmdlet](get-help-for-a-cmdlet.md): using `Get-Help` against the module.

## Practical

* [Tips](tips.md): assorted small recipes.
* [Verbose logging](verbose-logging.md): turning on diagnostic output.
