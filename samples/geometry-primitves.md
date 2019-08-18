# Geometry primitves

```text
function vpoint([double] $x,[double] $y)
{
    New-Object VisioAutomation.Geometry.Point($x,$y)
}

function vrect([double] $x0,[double] $y0, [double] $x1,[double] $y1)
{
    New-Object VisioAutomation.Geometry.Rectangle($x0,$y0,$x1,$y1)
}


```

To create a point

```text
vpoint 1 2
```

To create an array of points

```text
$points = @(
    vpoint 1 2
    vpoint 3 4
    vpoint 4 6
)
```

To create a rectangle

```text
vrect 1 2 3 4
```



