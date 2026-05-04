# Pages

A **page** is one canvas surface inside a Visio document. A document has at least one page (the *active* page) and can have many. Most page-targeted cmdlets default to the active page when `-Page` is omitted.

* [`Copy-VisioPage`](invoke-visioduplicate-page.md) &mdash; duplicate a page within the same document or into another document.
* [`Export-VisioPage`](export-visiopage.md) &mdash; export a single page to an image or HTML file.
* [`Format-VisioPage`](format-visiopage.md) &mdash; change page-level layout: size, orientation, fit-to-contents, background page, auto-layout.
* [`Get-VisioPage`](get-visiopage.md) &mdash; enumerate pages by name (with wildcards), by Visio ID, or just the active one.
* [`Measure-VisioPage`](measure-visiopage.md) &mdash; return `PageDimensions` records (width, height, margins) for one or more pages.
* [`New-VisioPage`](new-visiopage.md) &mdash; add a new page to a document, optionally pre-sized and pre-named.
* [`Remove-VisioPage`](remove-visiopage.md) &mdash; delete one or more pages.
* [`Select-VisioPage`](select-visiopage-tbd.md) &mdash; make a specific page the active one.

The PageSheet of a page is its ShapeSheet equivalent &mdash; see the related [PageCells](../pagecells.md) section for [`New-VisioPageCells`](new-visiopagecells.md) / [`Set-VisioPageCells`](set-visiopagecells.md), which write to the PageSheet.
