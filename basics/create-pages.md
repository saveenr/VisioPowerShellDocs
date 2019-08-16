# Create pages

The `New-VisioPage` cmdlet creates a new page

You can specify the height and width directly as you create the page

```text
New-VisioDocument
New-VisioPage -Name "HelloWorld" -Width 5 -Height 10
```

### Using PageCells to format the page

For width and height and other properties you can control them by passing in a PageCells object.

```text
New-VisioApplication
New-VisioDocument


$page_cells = New-VisioPageCells

$page_cells.PageHeight = "5 in"
$page_cells.PageHeight = "10 in"
$page_cells.PrintLeftMargin = "0 in"

New-VisioPage -Name "HelloWorld" -Cells $page_cells -Verbose
```



