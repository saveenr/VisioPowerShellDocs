# Get-VisioMaster



```text
Import-Module Visio

New-VisioApplication
New-VisioDocument

$basic_u = Open-VisioDocument "basic_u.vss"
$master = Get-VisioMaster -Name "Rectangle" -Document $basic_u
$points = New-Object VisioAutomation.Geometry.Point(4,5)
$shape = New-VisioShape -Master $master -Position $points

Set-VisioText "Hello World" -Shape $shape
```



Retrieve masters the current document

```text
Get-VisioMaster
```

Retrieve masters from a specific document

```text
Get-VisioMaster -Document $doc
```

Retrieve from the current document

```text
Get-VisioMaster -Name "Rectangle"
```

Retrieve from a specific document

```text
Get-VisioMaster -Name "Rectangle" -Document $doc
```





