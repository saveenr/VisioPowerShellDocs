# Format-VisioWindow



The `Format-VisioWindow` command controls the Zoom level of the active window.

#### Zoom to objects in a drawing <a id="zoom-to-objects-in-a-drawing"></a>

The `-To` parameter zooms the window relative to the active page or selection.

```text
Format-VisioWindow -ZoomTo Page
Format-VisioWindow -ZoomTo PageWidth
Format-VisioWindow -ZoomTo Selection
```

#### Zoom to a specific zoom level <a id="zoom-to-a-specific-zoom-level"></a>

The `-Value` parameter sets the zoom value directly. Visio's zoom value is a positive floating point number where 1.0 represents 100% zoom. Values greater than 1 means "Zoom in" and values less then 1 mean "Zoom out".

```text
Format-VisioWindow -Zoom 2.0  # Zoom in to 200% zoom
Format-VisioWindow -Zoom 1.0  # Zoom to 100% zoom
Format-VisioWindow -Zoom 0.5  # Zoom out to 50% zoom
Format-VisioWindow -Zoom 0.25 # Zoom out to 20% zoom
```

#### Incrementally changing the zoom <a id="incrementally-changing-the-zoom"></a>

The `-ValueRelative` parameter allows you to change the zoom in increments without having to specify an exact value. To zoom in by 10% of the current value use 1.1.

```text
Format-VisioWindow -ZoomRelative 1.1 # Zoom in by 10%
Format-VisioWindow -ZoomRelative 0.9 # Zoom out by 10%
```

