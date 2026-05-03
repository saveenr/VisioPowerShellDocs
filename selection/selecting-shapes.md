# Selecting shapes

#### Select all shapes <a href="#select-all-shapes" id="select-all-shapes"></a>

```
Select-VisioShape All
```

#### Selecting specific shapes <a href="#selecting-specific-shapes" id="selecting-specific-shapes"></a>

```
New-VisioRectangle 0 0 1 1
$shapes += New-VisioRectangle 0 0 1 1
$shapes += New-VisioRectangle 0 0 2 3

Select-VisioShape $shapes
```

You can pass in IDs of shapes

```
New-VisioRectangle 0 0 1 1
$shapes += New-VisioRectangle 0 0 1 1
$shapes += New-VisioRectangle 0 0 2 3
$shapeids = $shapes | ForEach-Object{ $_.ID }
Select-VisioShape $shapeids
```

#### &#x20;<a href="#deselect-all-shapes-clear-selection" id="deselect-all-shapes-clear-selection"></a>

#### &#x20;<a href="#invert-the-selection" id="invert-the-selection"></a>
