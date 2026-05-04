# Out-VisioApplication

The **Out-VisioApplication** cmdlet renders a layout / model object into the bound Visio application as a real Visio drawing. It accepts five different model types via the pipeline; the cmdlet picks the right rendering path based on what came in.

This is the rendering endpoint for the *automatic-diagram* family ([Org charts from XML](../../automatic-diagrams/drawing-org-charts.md), [Directed graphs from code](../../automatic-diagrams/drawing-directed-graphs.md), etc.) &mdash; you build a model object, then pipe it here.

## Syntax

```powershell
# Org chart
Out-VisioApplication [-OrgChart] <OrgChartDocument>

# Grid layout
Out-VisioApplication [-GridLayout] <GridLayout>

# Directed graph
Out-VisioApplication [-DirectedGraphDocument] <DirectedGraphDocument>

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
| `-DataTableModel` | `DataTableModel` | Yes | datatable | A data-table model. |
| `-XmlModel` | `XmlModel` | Yes | systemxmldoc | An XML-document model. |

The cmdlet throws if no Visio application is currently bound.

## Examples

### Render an XML directed graph

```powershell
$dgdoc = Import-VisioModel "graph.xml"
$dgdoc | Out-VisioApplication
```

### Render an org chart

```powershell
$orgchart = Import-VisioModel "people.xml"
$orgchart | Out-VisioApplication
```

## See also

* [Automatic diagrams](../../automatic-diagrams/README.md) &mdash; building the model objects this cmdlet consumes.
* `Import-VisioModel` (covered in the [Other cmdlets](../other-cmdlets.md) note).
