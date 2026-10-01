# Automatic diagrams

The Visio PowerShell module can generate diagrams from a high-level description rather than by drawing each shape individually. You build a model object (an org chart, a directed graph, a grid, a data table), then pass it to [`Out-VisioApplication`](../cmdlets/visioapplication/out-visioapplication.md), which renders it onto a real Visio page.

The model families currently documented:

* [Org charts from XML](drawing-org-charts.md): build an org-chart structure in XML, load it with `Import-VisioModel`, and render it.
* [Directed graphs from code](drawing-directed-graphs.md): construct a `DirectedGraphDocument` programmatically.
* [Directed graphs from XML](directed-graphs-from-xml/README.md): describe the graph in XML and let the module build the model. Includes several worked examples.
* [Grids](drawing-grids.md): place shapes in rows and columns, with per-column widths and per-row heights.
* [Data tables](drawing-data-tables.md): draw a `DataTable` as a grid of cells.
* [XML structure trees](drawing-xml-models.md): draw the element structure of any XML document as a tree.

The endpoint cmdlet is shared:

* [`Out-VisioApplication`](../cmdlets/visioapplication/out-visioapplication.md): renders any of the supported model types (`OrgChartDocument`, `DirectedGraphDocument`, `GridLayout`, `DataTableModel`, `XmlModel`) into the bound Visio application. All accept pipeline input.
* [`Import-VisioModel`](../cmdlets/other-cmdlets.md): loads an XML file and detects the model type from the root element. Documented in the [Other cmdlets](../cmdlets/other-cmdlets.md) note.
