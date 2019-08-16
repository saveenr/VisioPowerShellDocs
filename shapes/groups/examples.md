# Examples



#### Example 1 <a id="example-1"></a>

```text
Import-Module Visio
$visio = New-VisioApplication
$doc = New-VisioDocument
$stencil = Open-VisioDocument "basic_u.vss"

$master1 = Get-VisioMaster "Rounded Rectangle" $stencil 

# Drop multiple shapes at the same time
$shapes = New-VisioShape $master1 -Points 1,5.2,3,5.2,5,5.2

#Ensure that Nothing is Selected - just to demonstrate this feature
Select-VisioShape -Operation None

#Select the first and third shapes dropped
Select-VisioShape -Shapes $shapes[0],$shapes[2]

# Group the selected shapes
$g1 = New-VisioGroup

# Ungroup them
Split-VisioShape -Shapes $g1

# Group by specifying the shapes (ignore whatever is selected)
$g1 = Join-VisioShape -Shapes $shapes[0],$shapes[1]
```

