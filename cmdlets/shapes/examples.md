# Examples of Join-VisioShape and Split-VisioShape

## Example 1

```powershell
Import-Module Visio

$visio   = New-VisioApplication
$doc     = New-VisioDocument
$stencil = Open-VisioDocument "basic_u.vss"

$master1 = Get-VisioMaster "Rounded Rectangle" -Document $stencil

# Drop multiple shapes at the same time
$points = @(
    New-VisioPoint 1 5.2
    New-VisioPoint 3 5.2
    New-VisioPoint 5 5.2
)
$shapes = New-VisioShape -Master $master1 -Position $points

# Clear the selection -- just to demonstrate this feature
Select-VisioShape SelectNone

# Select the first and third shapes dropped
Select-VisioShape -Shapes $shapes[0],$shapes[2]

# Group the selected shapes
$g1 = Join-VisioShape

# Ungroup them
Split-VisioShape -Shape $g1

# Group by specifying the shapes (ignore whatever is selected)
$g1 = Join-VisioShape -Shape $shapes[0],$shapes[1]
```
