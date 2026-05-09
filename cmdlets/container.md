# Container

A **container** in Visio is a special shape that visually groups other shapes: the contained shapes move with it, paste with it, and report it as their parent. Unlike a group, members can still be selected and edited individually.

The PowerShell module exposes one container cmdlet:

* [`New-VisioContainer`](#new-visiocontainer): drop a container master around the currently selected shapes.

## New-VisioContainer

`New-VisioContainer` drops a container master from a stencil onto the active page. Whatever shapes are **selected** at the moment the cmdlet runs become members of the new container.

`-Master` is required and must be an `IVisio.Master`. Get it from a container stencil with [`Get-VisioMaster`](master/get-visiomaster.md).

### Example: wrap two shapes in a container

```powershell
Import-Module Visio

New-VisioApplication
New-VisioDocument

# Open a regular stencil and drop two rectangles
$basic_u = Open-VisioDocument "basic_u.vss"
$rect_m  = Get-VisioMaster "Rectangle" -Document $basic_u

$shape_a = New-VisioShape -Master $rect_m -Position (New-VisioPoint 2 2)
$shape_b = New-VisioShape -Master $rect_m -Position (New-VisioPoint 5 2)

# Open the container stencil and grab a container master
$cont_u    = Open-VisioDocument "SDCONT_U.VSSX"
$cont_m    = Get-VisioMaster "Container 1" -Document $cont_u

# Select the shapes you want inside the container, then drop it
Select-VisioShape -Shape $shape_a,$shape_b
$container = New-VisioContainer -Master $cont_m
```

The cmdlet returns the new container shape.

### Notes

* The drop uses Visio's native container API, so the result is a real Visio container (`msvStructureType = "Container"`), not just a backdrop shape.
* If nothing is selected when the cmdlet runs, the container is dropped empty.
* Container stencil filenames vary by Visio version. `SDCONT_U.VSSX` is the typical Visio 2013+ Universal-units container stencil.

## On the C# side

These cmdlets wrap the [`client.Container`](https://saveenr.gitbook.io/visioautomation/visio-scripting/container) command group on the VisioAutomation gitbook. See [VisioScripting.Client](https://saveenr.gitbook.io/visioautomation/visio-scripting) for the full facade index.
