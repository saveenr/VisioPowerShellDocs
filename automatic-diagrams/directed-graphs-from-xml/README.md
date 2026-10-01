# Directed graphs from XML



#### Draw a directed graph from XML <a href="#draw-a-directed-graph-from-xml" id="draw-a-directed-graph-from-xml"></a>

```
$dg = Import-VisioModel c:\foo.xml
$dg | Out-VisioApplication
```

Notes:

* `Import-VisioModel` takes a mandatory, positional `-Filename` parameter. It handles XML files whose root element is `<directedgraph>` or `<orgchart>`; any other root throws.
* `Out-VisioApplication` needs an attached Visio application. Run `New-VisioApplication` first; otherwise it throws "A Visio Application Instance is not attached".
* The graph is drawn into a new document created from the document's template (the default template), with one page per `<page>` element. It is not drawn onto the current page.







