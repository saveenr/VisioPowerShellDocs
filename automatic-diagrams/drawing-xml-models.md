# XML structure trees

An `XmlModel` draws the **structure** of an XML document as a tree: one node per element, joined by connectors. It is a quick way to see how a document is nested. Pass it to [`Out-VisioApplication`](../cmdlets/visioapplication/out-visioapplication.md).

```powershell
Import-Module Visio
New-VisioDocument | Out-Null

$xml = New-Object System.Xml.XmlDocument
$xml.LoadXml('<root><child1><leaf/></child1><child2/></root>')

$model = New-Object VisioAutomation.Models.Data.XmlModel
$model.XmlDocument = $xml

$model | Out-VisioApplication
```

This draws a top node labelled `#document` with `child1` and `child2` below it, and `leaf` below `child1`.

## What to expect

* The tree is drawn on the **current page** of the active document. A Visio application and document must already exist.
* Only **element names** are drawn. Attributes, text content, comments and processing instructions are not.
* The top node is labelled `#document`. It stands in for the document element: the document element's own name (`root` above) is not drawn, and the nodes below `#document` are its child elements.

This is different from the [directed graph XML](directed-graphs-from-xml/README.md) and [org chart XML](drawing-org-charts.md) formats, which describe a diagram and are loaded with `Import-VisioModel`. An `XmlModel` is built from any XML document and only visualizes its shape.

For the object model and the C# API, see [XML model](https://saveenr.gitbook.io/visioautomation/models/xml-model) in the VisioAutomation docs.
