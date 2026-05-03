# Geometry primitves

In order to use the VisioPS module, you'll have to eventually use Geometric primitives - points and rectangles - with the cmdlets.

### Points

A point has primitive type `VisioAutomation.Geometry.Point`. They have an X,Y coordinate.

#### Create a single Point

You can create a point primitive with the **New-VisioPoint** cmdlet.

```
New-VisioPoint 1 2
```

You can directly create the type with **New-Object**.

```
New-Object VisioAutomation.Geometry.Point(1,2)
```

#### Create an array of points

```
$points = @(
    New-VisioPoint 1 2
    New-VisioPoint 3 4
    New-VisioPoint 4 6
)
```

### Rectangles

The Rectangle primitive has type `VisioAutomation.Geometry.Rectangle`. It has is defined by four numbers (Left, Bottom, Right, Top).

**Constraints:**

* Left must always be less than or equal to Right
* Bottom must always be less than or equal to Top

#### Create a single rectangle

To create a rectangle

```
New-VisioRectangle 1 2 3 4
```

Or you can use New-Object

```
New-Object VisioAutomation.Geometry.Rectangle(1,2,3,4)
```

#### Create an array of Rectangles

```
$rects = @(
    New-VisioRectangle 1 2 3 4
    New-VisioRectangle 3 4 5 6
)

```
