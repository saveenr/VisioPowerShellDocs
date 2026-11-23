# Out-VisioApplication

The **Out-VisioApplication** cmdlet renders a layout / model object into the bound Visio application as a real Visio drawing. It accepts five different model types via the pipeline; the cmdlet picks the right rendering path based on what came in.

This is the rendering endpoint for the *automatic-diagram* family ([Org charts from XML](../../automatic-diagrams/drawing-org-charts.md), [Directed graphs from code](../../automatic-diagrams/drawing-directed-graphs.md), etc.): you build a model object, then pipe it here.

## Syntax

```powershell
# Org chart
Out-VisioApplication [-OrgChart] <OrgChartDocument>

# Grid layout
Out-VisioApplication [-GridLayout] <GridLayout>

# Directed graph
Out-VisioApplication [-DirectedGraphDocument] <DirectedGraphDocument> [-DirectedGraphStyling <DirectedGraphStyling>]

# Data-table model
Out-VisioApplication [-DataTableModel] <DataTableModel>

# XML model
Out-VisioApplication [-XmlModel] <XmlModel>
```

All five parameters accept pipeline input.

## Parameters

| Parameter | Type | Required | Parameter set | Description |
| --- | --- | --- | --- | --- |
| `-OrgChart` | `OrgChartDocument` | Yes | orgchart | An org-chart document model. |
| `-GridLayout` | `GridLayout` | Yes | grid | A grid-layout model. |
| `-DirectedGraphDocument` | `DirectedGraphDocument` | Yes | directedgraph | A directed-graph document model. |
| `-DirectedGraphStyling` | `DirectedGraphStyling` | No | directedgraph | The master and stencil used for the edges (connectors). Defaults to the `Dynamic Connector` master from `connec_u.vss`. Only valid with `-DirectedGraphDocument`. Added in module 5.1.0. |
| `-DataTableModel` | `DataTableModel` | Yes | datatable | A data-table model. |
| `-XmlModel` | `XmlModel` | Yes | systemxmldoc | An XML-document model. |

The cmdlet throws if no Visio application is currently bound.

## Where the output goes

The five parameter sets do not all render to the same place:

| Input | Where it is drawn |
| --- | --- |
| `-DirectedGraphDocument` | Into a **new document** created from the document's template, with one page per layout in the graph. The current document is not used. |
| `-OrgChart` | Into a **new document** created from Visio's Organization Chart template. The current document is not used, and no document needs to be open. Before module 5.1.0, `-OrgChart` failed with an error when no document and page were open. |
| `-GridLayout`, `-DataTableModel`, `-XmlModel` | Onto the **current page** of the active document. |

A directed graph is drawn into a new document because a `DirectedGraphDocument` can hold several layouts, each rendered on its own page. If you need a single directed graph on the page you already have open, render it with `MsaglRenderer` directly; see [Directed graphs from code](../../automatic-diagrams/drawing-directed-graphs.md).

## Examples

### Render an XML directed graph

```powershell
$dgdoc = Import-VisioModel "graph.xml"
$dgdoc | Out-VisioApplication
```

### Draw a directed graph with a different edge master

Added in module 5.1.0. `DirectedGraphStyling` has two fields, `EdgeMasterName` and `EdgeStencilName`. Set them to use another connector master for every edge:

```powershell
$styling = New-Object VisioAutomation.Models.Layouts.DirectedGraph.DirectedGraphStyling
$styling.EdgeStencilName = "connec_u.vss"
$styling.EdgeMasterName = "Dynamic Connector"

$dgdoc = Import-VisioModel "graph.xml"
$dgdoc | Out-VisioApplication -DirectedGraphStyling $styling
```

Unreleased: added after module 5.1.0. If the document carries its own connector styling, `Out-VisioApplication` uses that instead of `-DirectedGraphStyling`. In directed graph XML, set `connectormaster` and `connectorstencil` on `<documentoptions>`; a connector's own `master` and `stencil` attributes win over both. Use `-DirectedGraphStyling` for documents that do not set their own.

### Render an org chart

```powershell
$orgchart = Import-VisioModel "people.xml"
$orgchart | Out-VisioApplication
```

## See also

* [Automatic diagrams](../../automatic-diagrams/README.md): building the model objects this cmdlet consumes, including [grids](../../automatic-diagrams/drawing-grids.md), [data tables](../../automatic-diagrams/drawing-data-tables.md) and [XML structure trees](../../automatic-diagrams/drawing-xml-models.md).
* `Import-VisioModel` (covered in the [Other cmdlets](../other-cmdlets.md) note).
