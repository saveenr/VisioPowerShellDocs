# Pages

A **page** is one canvas surface inside a Visio document. A document has at least one page (the *active* page) and can have many. Most page-targeted cmdlets default to the active page when `-Page` is omitted.

* [`Copy-VisioPage`](invoke-visioduplicate-page.md): duplicate a page within the same document or into another document.
* [`Export-VisioPage`](export-visiopage.md): export a single page to an image or HTML file.
* [`Format-VisioPage`](format-visiopage.md): change page-level layout: size, orientation, fit-to-contents, background page, auto-layout.
* [`Get-VisioPage`](get-visiopage.md): enumerate pages by name (with wildcards), by Visio ID, or just the active one.
* [`Measure-VisioPage`](measure-visiopage.md): return `PageDimensions` records (width, height, margins) for one or more pages.
* [`New-VisioPage`](new-visiopage.md): add a new page to a document, optionally pre-sized and pre-named.
* [`Remove-VisioPage`](remove-visiopage.md): delete one or more pages.
* [`Select-VisioPage`](select-visiopage-tbd.md): make a specific page the active one.

The PageSheet of a page is its ShapeSheet equivalent; see the related [PageCells](../pagecells.md) section for [`New-VisioPageCells`](new-visiopagecells.md) / [`Set-VisioPageCells`](set-visiopagecells.md), which write to the PageSheet.

## On the C# side

These cmdlets wrap the [`client.Page`](https://saveenr.gitbook.io/visioautomation/visio-scripting/page) command group on the VisioAutomation gitbook. See [VisioScripting.Client](https://saveenr.gitbook.io/visioautomation/visio-scripting) for the full facade index.
