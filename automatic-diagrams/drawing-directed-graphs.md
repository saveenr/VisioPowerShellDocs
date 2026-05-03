# Directed graphs from code

```
Set-StrictMode -Version 2
#$ErrorActionPreference="Stop"
import-module Visio

# Load the needed DLLs
$sc = Get-VisioClient
#$sc.Assemblies | %{ Add-Type -Path $_ }​

$d = New-Object VisioAutomation.Models.Layouts.DirectedGraph.DirectedGraphLayout

$n1 = $d.AddNode("1", "Node1", "BASIC_U.VSS", "Rectangle")
$n2 = $d.AddNode("2", "Node2", "BASIC_U.VSS", "Rounded Rectangle")
$c1 = $d.AddEdge("3", $n1, $n2, "hello world", [VisioAutomation.Models.ConnectorType]::RightAngle)

$options=New-Object VisioAutomation.Models.Layouts.DirectedGraph.MsaglOptions

$renderer = New-Object VisioAutomation.Models.Layouts.DirectedGraph.MsaglRenderer
New-VisioApplication
New-VisioDocument
$p = New-VisioPage

$renderer.LayoutOptions = $options
$renderer.Render( $p, $d )
```

#### &#x20;<a href="#draw-a-directed-graph-from-xml" id="draw-a-directed-graph-from-xml"></a>
