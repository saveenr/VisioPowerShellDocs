# Draw basic shapes



### Drawing shapes without masters <a id="drawing-shapes-without-masters"></a>

The best way to use Visio is to "Drop Masters" with the `New-VisioShape` cmdlet. However, in some cases in may be more convenient to draw simple shapes without using masters.

```text
$s1 = New-VisioShape Rectangle 0,0,1,2
$s2 = New-VisioShape Line 1,2,5,8
$s3 = New-VisioShape Oval 0,0,3,6
$s4 = New-VisioShape Bezier 0,0,1,2,2,3,4,0
$s5 = New-VisioShape Polyline 0,0,1,2,2,3,4,0
```

