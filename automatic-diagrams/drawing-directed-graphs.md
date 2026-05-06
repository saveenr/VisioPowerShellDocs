# Directed graphs from code

```powershell
Set-StrictMode -Version 2
Import-Module Visio

$d = New-Object VisioAutomation.Models.Layouts.DirectedGraph.DirectedGraphLayout

$n1 = $d.AddNode("1", "Node1", "BASIC_U.VSS", "Rectangle")
$n2 = $d.AddNode("2", "Node2", "BASIC_U.VSS", "Rounded Rectangle")
$c1 = $d.AddEdge("3", $n1, $n2, "hello world", [VisioAutomation.Models.ConnectorType]::RightAngle)

$options  = New-Object VisioAutomation.Models.Layouts.DirectedGraph.MsaglOptions
$renderer = New-Object VisioAutomation.Models.Layouts.DirectedGraph.MsaglRenderer

New-VisioApplication
New-VisioDocument
$p = New-VisioPage

$renderer.LayoutOptions = $options
$renderer.Render($p, $d)
```

## Adding custom properties to nodes

Each node returned from `$d.AddNode(...)` exposes a `CustomProperties` dictionary you can populate before rendering. The dictionary's values are `CustomPropertyCells` objects, the same record type used by the `Set-VisioCustomProperty` cmdlet.

The `Formula` field on `CustomPropertyCells` is a Visio formula, not a literal value (the field was named `Value` before 2026-05; the old name is preserved as an `[Obsolete]` alias). The recommended way to populate it is via the typed setters, which encode the formula correctly:

```powershell
$cp = New-Object VisioAutomation.Shapes.CustomPropertyCells
$cp.SetString("testVal")     # SetNumber, SetBool, SetDate, SetFormula also available

$dic = New-Object VisioAutomation.Shapes.CustomPropertyDictionary
$dic.Add("DisplayName", $cp)
$n1.CustomProperties = $dic
```

After `$renderer.Render($p, $d)`, the rendered shape carries the property correctly.

| Setter | What it does |
| --- | --- |
| `$cp.SetString("hello")` | Encodes as a Visio string literal. Sets `Type=0` (String). |
| `$cp.SetNumber(42)` | Numeric formula. Sets `Type=2` (Number). |
| `$cp.SetBool($true)` | `TRUE` or `FALSE`. Sets `Type=3` (Boolean). |
| `$cp.SetDate([datetime]::Now)` | Wraps in `DATETIME(...)`. Sets `Type=5` (Date). |
| `$cp.SetFormula("=...")` | Raw escape hatch. Writes the formula verbatim, leaves `Type` untouched. |

If you bypass the setters and assign directly to `$cp.Formula`, an unencoded string (`$cp.Formula = "testVal"`) raises an `ArgumentException` from `$renderer.Render` with a diagnostic pointing at the setters. The `Set-VisioCustomProperty` cmdlet handles encoding internally, so its callers don't need to think about any of this; this section applies only when you build a `DirectedGraphLayout` from code, as shown above.
