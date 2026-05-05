# Text

Each Visio shape can carry a single text string. The **Text** cmdlets read and write that text. Formatting the text (font, size, color, alignment) is a separate concern handled through ShapeSheet character cells; see [Set-VisioShapeCells for text](../shapecells/format-text.md).

* [`Get-VisioText`](get-visiotext.md): read the text of one or more shapes.
* [`Set-VisioText`](set-visiotext.md): set the text on one or more shapes (single string broadcast to every shape, or an array zipped position-for-position).
