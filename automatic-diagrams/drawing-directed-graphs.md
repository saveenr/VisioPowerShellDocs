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

There is one important gotcha: the `Value` (and `Label` / `Format` / `Prompt`) fields on `CustomPropertyCells` are Visio *formulas*, not literal values. Setting `$cp.Value = "testVal"` stores the formula `testVal` (no quotes), which Visio evaluates as a name reference, fails to resolve, and silently substitutes a default (typically `0`). To store a string literal, the formula needs to include the quotes.

Two ways to do that:

```powershell
# Option A: call EncodeValues() before adding to the dictionary.
# Quotes Value, Label, Format, and Prompt as needed.
$cp = New-Object VisioAutomation.Shapes.CustomPropertyCells
$cp.Value = "testVal"
$cp.EncodeValues()

$dic = New-Object VisioAutomation.Shapes.CustomPropertyDictionary
$dic.Add("DisplayName", $cp)
$n1.CustomProperties = $dic
```

```powershell
# Option B: pre-quote the formula yourself.
$cp = New-Object VisioAutomation.Shapes.CustomPropertyCells
$cp.Value = '"testVal"'

$dic = New-Object VisioAutomation.Shapes.CustomPropertyDictionary
$dic.Add("DisplayName", $cp)
$n1.CustomProperties = $dic
```

After `$renderer.Render($p, $d)`, the rendered shape carries the property correctly.

Numeric, boolean, and date values are not strings and don't need quoting; pass them as literals via the typed constructors:

```powershell
$cp_num  = New-Object VisioAutomation.Shapes.CustomPropertyCells 42
$cp_bool = New-Object VisioAutomation.Shapes.CustomPropertyCells $true
$cp_date = New-Object VisioAutomation.Shapes.CustomPropertyCells ([System.DateTime]::Now)
```

The `Set-VisioCustomProperty` cmdlet calls `EncodeValues()` internally, so its callers don't have to think about this. The model-level path (used here, when you build a `DirectedGraphLayout` from code) leaves it to the caller. [Issue #144](https://github.com/saveenr/VisioAutomation/issues/144) tracks options for making this more ergonomic.
