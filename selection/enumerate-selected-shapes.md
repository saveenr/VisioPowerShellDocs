# Enumerate selected shapes

#### Enumerate currently selected shapes <a href="#getting-currently-selected-shapes" id="getting-currently-selected-shapes"></a>

```
$shapes = Get-VisioShape
```

#### Get all shapes on page regardless of selection <a href="#get-all-shapes-on-page-regardless-of-selection" id="get-all-shapes-on-page-regardless-of-selection"></a>

```
$shapes = Get-VisioShape *
```

#### Get all shapes on page by name <a href="#get-all-shapes-on-page-by-name" id="get-all-shapes-on-page-by-name"></a>

```
$shapes = Get-VisioShape "Shapename"
```

NOTE: Wildcards are NOT supported

#### Get selected shapes included shapes inside groups <a href="#get-selected-shapes-included-shapes-inside-groups" id="get-selected-shapes-included-shapes-inside-groups"></a>

```
$shapes = Get-VisioShape -Recursive
```

