# Drop shape masters

### Overview

The recommended way to get shapes on a page is to _drop_ a _master_ from a _stencil_.

### **Dropping a master**

The following code shows the simplest case. It drops a "Rectangle" shape into the current page at position 4,5.

```
$basic_u = Open-VisioDocument "basic_u.vss"
$master = Get-VisioMaster "Rectangle" -Document $basic_u
$points = New-VisioPoint 4 5
$shape = New-VisioShape -Master $master -Position $points
```

### **Dropping a master multiple times**

```
$basic_u = Open-VisioDocument "basic_u.vss"
$master = Get-VisioMaster "Rectangle" -Document $basic_u
$points = @(
    New-VisioPoint 4 5
    New-VisioPoint 6 1
    New-VisioPoint 0 0
    )
$shapes = New-VisioShape -Master $master -Position $points

Set-VisioText -Text "Hello World" -Shape $shapes
```

### **Dropping multiple masters at the same time**

In this case, we want different masters dropped all at the same time

```
$basic_u = Open-VisioDocument "basic_u.vss"
$masters = Get-VisioMaster -Name "Rectangle","Triangle","Circle"  -Document $basic_u
$points = @(
    New-VisioPoint 4 5
    New-VisioPoint 6 1
    New-VisioPoint 0 0
    )
$shape = New-VisioShape -Master $masters -Position $points

Set-VisioText -Text "Hello World" -Shape $shape
```

The `New-VisioShape` cmdlet returns the dropped shapes as `IVisio.Shape` objects.

### **If your master is in a template, not a stencil**

If you point `Open-VisioDocument` at a template (`.vst` / `.vstx`) and `Get-VisioMaster` comes back empty, that's because templates usually don't carry their own masters. Instead, the template references one or more companion stencils that Visio auto-loads alongside it. The masters live on those companion documents.

The simplest fix is to open the companion stencil directly. For example, the Active Directory template `actdir_u.vstx` has its shapes in `actdir_u.vssx`:

```
$stencil = Open-VisioDocument "actdir_u.vssx"
$g       = Get-VisioMaster -Name "Group" -Document $stencil
```

If you don't know the companion filename, walk `Application.Documents` after opening the template to find the loaded stencil. See [Templates vs. stencils](../cmdlets/documents/open-visiodocument.md#templates-vs-stencils) on the `Open-VisioDocument` page for the full pattern.
