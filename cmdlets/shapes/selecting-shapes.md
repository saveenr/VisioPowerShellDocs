# Select-VisioShape

#### Select all shapes <a id="select-all-shapes"></a>

```text
Select-VisioShape All
```

#### Selecting specific shapes <a id="selecting-specific-shapes"></a>

```text
New-VisioRectangle 0 0 1 1
$shapes += New-VisioRectangle 0 0 1 1
$shapes += New-VisioRectangle 0 0 2 3

Select-VisioShape $shapes
```

You can pass in IDs of shapes

```text
New-VisioRectangle 0 0 1 1
$shapes += New-VisioRectangle 0 0 1 1
$shapes += New-VisioRectangle 0 0 2 3
$shapeids = $shapes | ForEach-Object{ $_.ID }
Select-VisioShape $shapeids
```

####  <a id="deselect-all-shapes-clear-selection"></a>

####  <a id="invert-the-selection"></a>

