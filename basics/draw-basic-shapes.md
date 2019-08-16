# Draw basic shapes

The best way to use Visio is to "Drop Masters" with the `New-VisioShape` cmdlet. However, in some cases it is more convenient to draw simple shapes manually without using masters.

```text
# Shapes built from rectangular bounding boxes

$rect =  New-Object VisioAutomation.Geometry.Rectangle(0,0,1,2)
$s1 = New-VisioShape -Rectangle -BoundingBox $rect

$rect =  New-Object VisioAutomation.Geometry.Rectangle(0,0,3,6)
$s = New-VisioShape -Oval -BoundingBox $rect

# Shapes build from a a starting and ending point

$pstart = New-Object VisioAutomation.Geometry.Point(1,2)
$pend = New-Object VisioAutomation.Geometry.Point(5,8)
$s2 = New-VisioShape -Line -From $pstart -To $pend




# Shapes build from a series of points


$points = @(
    New-Object VisioAutomation.Geometry.Point(0,0)
    New-Object VisioAutomation.Geometry.Point(1,2)
    New-Object VisioAutomation.Geometry.Point(2,3)
    New-Object VisioAutomation.Geometry.Point(4,0)
    )


$s2 = New-VisioShape -Bezier -Points $points
$s5 = New-VisioShape -Polyline -Points $points
```

This method is much slower if you have to draw multiple shapes.

