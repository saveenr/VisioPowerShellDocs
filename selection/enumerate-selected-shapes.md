# Enumerate selected shapes

#### Enumerate currently selected shapes <a id="getting-currently-selected-shapes"></a>

```text
$shapes = Get-VisioShape
```

#### Get all shapes on page regardless of selection <a id="get-all-shapes-on-page-regardless-of-selection"></a>

```text
$shapes = Get-VisioShape *
```

#### Get all shapes on page by name <a id="get-all-shapes-on-page-by-name"></a>

```text
$shapes = Get-VisioShape "Shapename"
```

NOTE: Wildcards are NOT supported

#### Get selected shapes included shapes inside groups <a id="get-selected-shapes-included-shapes-inside-groups"></a>

```text
$shapes = Get-VisioShape -Recursive
```



