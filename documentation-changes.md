# Documentation changes

This page lists notable changes to the **Visio PowerShell** documentation, newest first, so returning readers can see what's new without re-reading every page.

For the module's own release notes, see [Release history](developer-info/release-history.md).

## 2026-11: Visio PowerShell 5.1.0 release

* [Out-VisioApplication](cmdlets/visioapplication/out-visioapplication.md)
  * `-DirectedGraphStyling` is now marked as added in 5.1.0 (it was marked unreleased).
  * The output table now shows that `-OrgChart` draws into a **new document**.
  * `-OrgChart` no longer needs an open document (5.1.0).
* Updated [Version compatibility](developer-info/version-compatibility.md) and [Release history](developer-info/release-history.md) for 5.1.0.

## 2026-11: Visio PowerShell 5.0.0 release

* The module now requires **.NET Framework 4.7.2** on the host.
* Updated [Version compatibility](developer-info/version-compatibility.md) and [Release history](developer-info/release-history.md) for 5.0.0.
  * Version compatibility also has a note for older Windows images and a corrected 4.8.0 changelog link.
  * Release history notes that validation failures in eight cmdlets now stop the cmdlet even without `$ErrorActionPreference = 'Stop'`.

## 2026-10: Visio PowerShell 4.8.0 release sweep

* Notes that said "after 4.7.3" are now plain version statements on these pages:
  * [Get-VisioPage](cmdlets/pages/get-visiopage.md)
  * [New-VisioDocument](cmdlets/documents/new-visiodocument.md)
  * [Drawing data tables](automatic-diagrams/drawing-data-tables.md)
  * [Drawing XML models](automatic-diagrams/drawing-xml-models.md)
* Updated [Version compatibility](developer-info/version-compatibility.md) and [Release history](developer-info/release-history.md) for 4.8.0.

## 2026-10: New-VisioDocument -Template

Page: [New-VisioDocument](cmdlets/documents/new-visiodocument.md). Shipped in 4.8.0.

* `-Template` now creates the new document **from** the template, with its page setup, styles and docked stencils.
* A stencil passed to `-Template` is rejected.
* In 4.7.3 and earlier, the template was opened as a separate docked stencil beside a blank drawing.
* The page explains how to move a script to `-Stencil` ([#229](https://github.com/saveenr/VisioAutomation/issues/229)).

## 2026-10: Get-VisioPage -ID and -Index

Page: [Get-VisioPage](cmdlets/pages/get-visiopage.md). Shipped in 4.8.0.

* `-ID` is now a real Visio page ID.
* New `-Index` parameter selects pages by position, counting from 1.
* In 4.7.3 and earlier, `-ID` silently treated its numbers as positions.
* The page explains how to move a script from `-ID` to `-Index` ([#232](https://github.com/saveenr/VisioAutomation/issues/232)).

## 2026-05: Version compatibility reference

* New page: [Version compatibility](developer-info/version-compatibility.md), under **Developer Info**.
* For each module version it shows:
  * the supported PowerShell host
  * the bundled DLL target framework
  * the Visio PIA baseline
  * the matching `VisioAutomation2010` NuGet release
* Sources:
  * 4.6.1 to 4.7.2: the `Visio.psd1` and csproj at each tag.
  * Older rows: best effort, from the [Release history](developer-info/release-history.md).
* Notes that the manifest still declares `PowerShellVersion = '2.0'` for historical reasons. The real minimum was PowerShell 5.1 on .NET Framework 4.5.2.
* Links to the [.NET-side compatibility table](https://saveenr.gitbook.io/visioautomation/version-compatibility). Closes [#161](https://github.com/saveenr/VisioAutomation/issues/161).

## 2026-05: Custom-property typed setters

Source issue: [#144](https://github.com/saveenr/VisioAutomation/issues/144).

* What changed in the library:
  * `CustomPropertyCells` has typed setters: `SetString`, `SetNumber`, `SetBool`, `SetDate`, `SetFormula`.
  * `UserDefinedCellCells` has `SetString` and `SetFormula`.
  * Each writes a correctly encoded Visio formula.
  * `Value` was renamed `Formula`. `Value` stays as an `[Obsolete]` alias.
* Who is affected:
  * Cmdlet users are not. `Set-VisioCustomProperty -Name "X" -Value "x"` works as before.
  * Scripts that build a `CustomPropertyCells` with `New-Object` and pass it through `-Cells`, or build a `DirectedGraphLayout` from code, see the change.
* Pages updated:
  * [drawing-directed-graphs.md](automatic-diagrams/drawing-directed-graphs.md): "Adding custom properties to nodes" now leads with `$cp.SetString("v")`, adds a setter table, and notes the new `ArgumentException` for unencoded `$cp.Formula = "..."`.
  * [set-visiocustomproperty.md](cmdlets/custom-properties/set-visiocustomproperty.md): the "Use the Cells form" example uses the typed setters.
* The per-type behavior details live on the .NET-side [Custom properties](https://saveenr.gitbook.io/visioautomation/custom-properties) page. These pages link there.
* Closes the thread that began with [#117](https://github.com/saveenr/VisioAutomation/issues/117).

## 2026-05: Custom properties on directed-graph nodes from code

Source issue: [#117](https://github.com/saveenr/VisioAutomation/issues/117).

* The problem: setting `$cp.Value = "testVal"` on a `CustomPropertyCells` made the property render as `0`.
* The cause: `Value`, `Label`, `Format` and `Prompt` are Visio **formulas**, not literals, so a bare word is read as an unresolved name.
* `Set-VisioCustomProperty` avoids this by calling `EncodeValues()` itself. Building a `DirectedGraphLayout` from code leaves that to you.
* Fix: [drawing-directed-graphs.md](automatic-diagrams/drawing-directed-graphs.md) has a new "Adding custom properties to nodes" section. It explains formula versus literal and shows two ways to store a string (`EncodeValues()` or pre-quoting).
* The same patch went into the .NET-side [Custom properties](https://saveenr.gitbook.io/visioautomation/custom-properties) page.

## 2026-05: Templates versus stencils

Source issue: [#102](https://github.com/saveenr/VisioAutomation/issues/102).

* The problem: opening a template (`.vst`, `.vstx`) with `Open-VisioDocument` gives a document whose `Masters` collection is usually empty, because the masters live on companion stencils that Visio loads alongside it.
* Pages updated:
  * `cmdlets/documents/open-visiodocument.md`: a callout at the top and a new "Templates vs. stencils" section with two ways to reach the masters (open the companion `.vssx`, or walk `Application.Documents`).
  * `basics/drop-masters.md`: a short "If your master is in a template, not a stencil" subsection.

## 2026-05: Runtime-failure pass

A scripted check of every PowerShell code block on the site. Each fix was verified against the 4.6.1 module.

* `technical-notes/use-visioautomation.md`
  * Replaced `Get-VisioScriptingClient` with `Get-VisioClient`.
  * Removed `$sc.Assemblies`, which does not exist.
  * Moved the geometry types to `VisioAutomation.Core` and renamed `SRCConstants` to `SrcConstants`.
  * Dropped the `Add-Type` loop, because `Import-Module Visio` already loads the assemblies.
* `cmdlets/pages/format-visiopage.md`: removed the same broken `Add-Type` loop.
* `cmdlets/custom-properties/examples.md`: fixed a `.Formula` that should have been `.Value`.
* `samples/draw-fill-patterns.md`
  * `New-VisioShape -Type Rectangle` is now `-Rectangle (New-VisioRectangle ...)`.
  * `-Shapes` is now `-Shape` on `Set-VisioText` and `Set-VisioShapeCells`.
* `cmdlets/shapes/enumerate-selected-shapes.md`: `Get-VisioShape` with no arguments returns every shape on the active page, not the selection. The page now says so.
* `cmdlets/shapecells/new-visioshapecells.md`: the property is `XFormPinX`, not `PinX`.

## 2026-05: Refresh against module 4.6.1

Every cmdlet page was aligned with the 4.6.1 module (released 2026-05-03).

### New cmdlet pages

* Shapes: [New-VisioShape](cmdlets/shapes/new-visioshape.md), [Remove-VisioShape](cmdlets/shapes/remove-visioshape.md)
* Page cells: [New-VisioPageCells](cmdlets/pages/new-visiopagecells.md), [Set-VisioPageCells](cmdlets/pages/set-visiopagecells.md)
* Shape cells: [Get-VisioShapeCells](cmdlets/shapecells/get-visioshapecells.md), [New-VisioShapeCells](cmdlets/shapecells/new-visioshapecells.md)
* Control handles (new section): [Get-VisioControl](cmdlets/control/get-visiocontrol.md), [New-VisioControl](cmdlets/control/new-visiocontrol.md), [Remove-VisioControl](cmdlets/control/remove-visiocontrol.md)
* All seven [VisioApplication cmdlets](cmdlets/visioapplication/): Close, Get, New, Out, Test, Undo, Redo
* Previously marked `[TBD]`: [Copy-VisioPage](cmdlets/pages/invoke-visioduplicate-page.md), [Select-VisioPage](cmdlets/pages/select-visiopage-tbd.md), [Get-VisioText](cmdlets/text/get-visiotext.md)
* [Other cmdlets](cmdlets/other-cmdlets.md): one page for the small utility cmdlets (`Get-VisioClient`, `Get-VisioLockCells`, `Import-VisioModel`, `Measure-VisioShape`, `New-VisioPoint`, `New-VisioRectangle`, `Select-VisioDocument`, `Test-VisioDocument`)

### Standard page layout

Every cmdlet page now has:

* a one-sentence intro with the cmdlet name in bold
* a **Syntax** block in `Get-Help -Syntax` style (one per parameter set)
* a **Parameters** table: name, type, required or not, description
* an **Examples** section
* a **See also** section

### New behavior documented (4.6.1)

* `Lock-VisioShape` and `Unlock-VisioShape`: the switches (`-Width`, `-Height`, `-MoveX` and so on) now take effect. In 4.6.0 and earlier they were silently ignored.
* `Export-VisioShape`: no longer needs `-Overwrite` to write to a fresh path. The "Known limitation" note is gone.
* `New-VisioShape`: `-Polyline` needs at least 2 points and `-Bezier` at least 4. The cmdlet now enforces this.
* The lock pages state the version requirement, so readers on older modules are not misled.

### Corrected examples

Many examples used cmdlets, parameters or values that do not exist:

* Cmdlets that do not exist:
  * `Set-VisioPage` became `Select-VisioPage`.
  * `Set-VisioDocument` became `Select-VisioDocument`.
  * `Get-VisioScriptingClient` became `Get-VisioClient`.
  * `New-VisioGroup` became `Join-VisioShape`.
* Parameters that do not exist:
  * `Export-VisioPage -AllPages` is now a `foreach` loop over `Get-VisioPage`.
  * `Get-VisioShape -Recursive` was removed.
  * `New-VisioShape -Masters X -Points Y,Z` is now `-Master $m -Position (New-VisioPoint X Y)`.
  * `Format-VisioShape -NudgeX` for vertical nudges is now `-NudgeY`.
  * `Format-VisioWindow` prose now uses `-ZoomTo`, `-Zoom` and `-ZoomRelative`.
* Values and types:
  * `Select-VisioShape` takes `SelectAll`, `SelectNone` and `InvertSelection`, not `All`, `None` and `Invert`.
  * `VisioAutomation.Geometry.Point` is `VisioAutomation.Core.Point`. Examples use `New-VisioPoint X Y`.

### Publishing to the PowerShell Gallery

* [Publish to PowerShell Gallery](developer-info/publishing-to-powershell-gallery.md) was rewritten after a real publish found several gotchas:
  * TLS 1.2
  * bugs in the in-box PowerShellGet 1.x
  * the PowerShell 5.1 versus 7 module path
  * `.ps1` file encoding
* It now points to the `Publish-VisioPSToGallery.ps1` release script and documents a quick path and a manual fallback.
