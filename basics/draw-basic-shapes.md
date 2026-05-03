# Draw basic shapes

The best way to use Visio is to "Drop Masters" with the `New-VisioShape` cmdlet. However, in some cases it is more convenient to draw simple shapes manually without using masters.

```
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"
$numcols = 6
$cellsep = 1.0
$cellwidth=1

Import-Module Visio
New-VisioApplication
New-VisioDocument

$d = $cellwidth + $cellsep
for ($i=0;$i -le 40;$i++) 
{
    $x = $i % $numcols 
    $y = [math]::floor($i / $numcols )
    $left = $x*$d
    $bottom = $y*$d
    $right = $left + $cellwidth
    $top = $bottom + $cellwidth
    $shape1_cells = New-VisioShapeCells
    $shape1_cells.FillForeground = "rgb(0,128,195)"
    $shape1_cells.FillBackground = "rgb(255,255,255)"
    $shape1_cells.FillPattern = $i
    $shape2_cells = New-VisioShapeCells
    $shape2_cells.FillPattern = 0
    $shape2_cells.LinePattern = 0
    $s1 = New-VisioShape -Rectangle (New-VisioRectangle $left $bottom $right $top)
    $s2 = New-VisioShape -Rectangle (New-VisioRectangle $left ($bottom-0.5) $right $bottom)
    Set-VisioText $i -Shape $s2
    Set-VisioShapeCells -Cells $shape1_cells -Shape $s1
    Set-VisioShapeCells -Cells $shape2_cells -Shape $s2
}
Format-VisioPage -BorderWidth 1.0 -BorderHeight 1.0 -FitContents
```

This method is much slower if you have to draw multiple shapes.
