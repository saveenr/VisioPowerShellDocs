# Enumerate shapes

#### Enumerate currently selected shapes on active page <a href="#getting-currently-selected-shapes" id="getting-currently-selected-shapes"></a>

```
Get-VisioShape -ActiveSelection
```

#### Get all shapes on active page <a href="#get-all-shapes-on-page-regardless-of-selection" id="get-all-shapes-on-page-regardless-of-selection"></a>

```
Get-VisioShape -Name * 
```

#### Get shapes by id

```
Get-VisioShape -Id 2
Get-VisioShape -Id 2,3
```





