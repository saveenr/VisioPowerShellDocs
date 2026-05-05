# Other cmdlets

The Visio module ships a few small or specialised cmdlets that don't have their own page in this guide. They are listed here so they're discoverable, with a one-line description of what each does. If you need full reference for one of them, run `Get-Help <cmdlet-name>` in your shell.

| Cmdlet | What it does |
| --- | --- |
| `Get-VisioClient` | Returns the underlying `VisioScripting.Client` object. Useful only when dropping down to the .NET API directly. |
| `Get-VisioLockCells` | Reads the lock-related ShapeSheet cells (`LockMoveX`, `LockSelect`, `LockTextEdit`, …) for one or more shapes. Returns a dictionary keyed by shape. |
| `Import-VisioModel` | Loads a directed-graph or org-chart XML file and renders it as a diagram. The richer scenarios are covered in [Automatic diagrams](../automatic-diagrams/README.md). |
| `Measure-VisioShape` | Returns size-and-position records (`ShapeDimensions`) for the given shapes. |
| `New-VisioPoint` | Constructs a `Point` value, e.g. `New-VisioPoint 4 5`. Used by many `New-VisioShape` examples. |
| `New-VisioRectangle` | Constructs a `Rectangle` value: `New-VisioRectangle Left Bottom Right Top`. Used by `New-VisioShape -Rectangle`/`-Oval`. |
| `Select-VisioDocument` | Activates a document so that subsequent cmdlets which target the "active document" use it. |
| `Test-VisioDocument` | Boolean. `True` if a document is currently open in the bound Visio application. |
