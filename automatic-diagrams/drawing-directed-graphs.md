# Directed graphs from code

```text
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

import-module Visio

# Load the needed DLLs
$sc = Get-VisioScriptingClient
$sc.Assemblies | %{ Add-Type -Path $_ }

$d = New-Object VisioAutomation.Models.Layouts.DirectedGraph.DirectedGraphLayout
$n1 = $d.AddShape("1", "Node1", "BASIC_U.VSS", "Rectangle")
$n2 = $d.AddShape("2", "Node2", "BASIC_U.VSS", "Rounded Rectangle")
$c1 = $d.AddConnection("3", $n1, $n2)
$c1.ConnectorType = [VisioAutomation.Shapes.ConnectorType]::RightAngle


$options = New-Object VisioAutomation.Models.Layouts.DirectedGraph.MSAGLLayoutOptions

New-VisioApplication
New-VisioDocument
$p = New-VisioPage

$d.Render($p, $options)
```

####  <a id="draw-a-directed-graph-from-xml"></a>

