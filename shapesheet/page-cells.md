# Page cells



These cmdlets work with the ShapeSheet of pages:

```text
New-VisioShapeCells
Get-VisioPageCells
Set-VisioShapeCells
```

#### Working with page cells <a id="working-with-page-cells"></a>

As shown below, the process is very similar to working with shapes

```text
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

New-VisioApplication
$doc = New-VisioDocument
$page = Get-VisioPage -ActivePage

$cells_dt = Get-VisioPageCells -Pages $page 

Write-Host $cells_dt

$new_cells = New-VisioPageCells 

$new_cells.PageHeight = 3
$new_cells.PageWidth = 6

Set-VisioPageCells -Cells $new_cells -Pages $pages
```

#### Querying multiple pages <a id="querying-multiple-pages"></a>

```text
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"

Import-Module Visio

New-VisioApplication
$doc = New-VisioDocument

# The doc already has one page, add four more empty pages
New-VisioPage | Out-Null
New-VisioPage | Out-Null
New-VisioPage | Out-Null
New-VisioPage | Out-Null

$pages = Get-VisioPage 

$pages_dt = Get-VisioPageCells -Pages $pages 

Write-Host $pages_dt
```

