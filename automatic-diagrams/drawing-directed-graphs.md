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

Render draws onto the page you pass it. To draw a loaded `DirectedGraphDocument` (for example the output of `Import-VisioModel`) use `Out-VisioApplication` instead. It needs an attached Visio application (run `New-VisioApplication` first; otherwise it throws "A Visio Application Instance is not attached"). It draws into a new document created from the document's template (the default template), with one page per `<page>` element, not onto the current page.

## Layout options

The layout is controlled by the `LayoutOptions` of the renderer. When you call `$renderer.Render($p, $d)` directly, set them on `$renderer.LayoutOptions`; the renderer does not read the options stored on the graph.

| Property | Default | What it does |
| --- | --- | --- |
| `Direction` | `TopToBottom` | Which way the graph flows: `TopToBottom`, `BottomToTop`, `LeftToRight` or `RightToLeft`. |
| `UseDynamicConnectors` | `$true` | `$true` uses Visio's dynamic connectors, which re-route when shapes move. `$false` keeps the geometry the layout engine computed. |
| `ScalingFactor` | `14` | Converts between inches and the layout engine's units. Node sizes are multiplied by it before layout, but the engine's own spacing is fixed, so a larger value gives tighter gaps relative to node size and a smaller value gives looser spacing. |
| `DefaultShapeSize` | `1.0 x 0.75` | A fallback node size in inches. In practice it does not apply: a node with no `Size` is laid out and drawn at the size of its master. Set `Size` on the node to override the master's size. |
| `PageBorderWidth` | `0.5 x 0.5` | Margin in inches around the finished drawing. |
| `EdgeLabelBoxSize` | `1.0 x 0.5` | Space in inches reserved for each edge's label, for every edge whether or not it has a label. Smaller values give tighter gaps between layers. Unreleased; see [Tightening the layout](#tightening-the-layout). |
| `LayerSeparation` | `$null` | Minimum distance in inches between layers. `$null` uses the layout engine's own default. Unreleased; see [Tightening the layout](#tightening-the-layout). |

This example lays the graph out left to right with routed connectors:

```powershell
Import-Module Visio

$d = New-Object VisioAutomation.Models.Layouts.DirectedGraph.DirectedGraphLayout
$n1 = $d.AddNode("1", "Node1", "BASIC_U.VSS", "Rectangle")
$n2 = $d.AddNode("2", "Node2", "BASIC_U.VSS", "Rectangle")
$n3 = $d.AddNode("3", "Node3", "BASIC_U.VSS", "Rectangle")
$c1 = $d.AddEdge("4", $n1, $n2, "", [VisioAutomation.Models.ConnectorType]::Straight)
$c2 = $d.AddEdge("5", $n2, $n3, "", [VisioAutomation.Models.ConnectorType]::Straight)

New-VisioApplication
New-VisioDocument
$p = New-VisioPage

$renderer = New-Object VisioAutomation.Models.Layouts.DirectedGraph.MsaglRenderer
$renderer.LayoutOptions.Direction = [VisioAutomation.Models.Layouts.DirectedGraph.MsaglDirection]::LeftToRight
$renderer.LayoutOptions.UseDynamicConnectors = $false
$renderer.Render($p, $d)
```

## Tightening the layout

`EdgeLabelBoxSize` and `LayerSeparation` are in current source and are an unreleased addition after VisioAutomation NuGet 3.0.0. A Visio PowerShell module built on the 3.0.0 library does not have these properties, and setting them there fails.

Every edge reserves room for a label whether or not it has one, which widens the gaps between layers. Shrinking `EdgeLabelBoxSize` reclaims that space, and `LayerSeparation` sets the minimum distance between layers directly. This lays the left-to-right graph out more tightly:

```powershell
Import-Module Visio

$d = New-Object VisioAutomation.Models.Layouts.DirectedGraph.DirectedGraphLayout
$n1 = $d.AddNode("1", "Node1", "BASIC_U.VSS", "Rectangle")
$n2 = $d.AddNode("2", "Node2", "BASIC_U.VSS", "Rectangle")
$n3 = $d.AddNode("3", "Node3", "BASIC_U.VSS", "Rectangle")
$c1 = $d.AddEdge("4", $n1, $n2, "", [VisioAutomation.Models.ConnectorType]::Straight)
$c2 = $d.AddEdge("5", $n2, $n3, "", [VisioAutomation.Models.ConnectorType]::Straight)

New-VisioApplication
New-VisioDocument
$p = New-VisioPage

$renderer = New-Object VisioAutomation.Models.Layouts.DirectedGraph.MsaglRenderer
$renderer.LayoutOptions.Direction = [VisioAutomation.Models.Layouts.DirectedGraph.MsaglDirection]::LeftToRight
$renderer.LayoutOptions.UseDynamicConnectors = $false
$renderer.LayoutOptions.EdgeLabelBoxSize = New-Object VisioAutomation.Core.Size(0.8, 0.12)
$renderer.LayoutOptions.LayerSeparation = 0.25
$renderer.Render($p, $d)
```

In this example the gap between neighboring nodes drops from about 3.1 inches (without the two settings) to about 1.5 inches, and the page from about 12.3 to 9.0 inches wide.

The same settings are available in directed graph XML as the `layerseparation`, `edgelabelboxwidth` and `edgelabelboxheight` attributes of `<renderoptions>`; see the [XML format](https://saveenr.gitbook.io/visioautomation/directed-graph-xml#renderoptions).

For the full object model, see [Directed graph](https://saveenr.gitbook.io/visioautomation/models/directed-graph) in the VisioAutomation docs.

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
