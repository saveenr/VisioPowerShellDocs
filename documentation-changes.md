# Documentation changes

This page summarizes notable changes to the **Visio PowerShell** documentation so returning readers can find what's new without re-reading every page.

For the underlying module's release notes, see [Release history](developer-info/release-history.md).

## 2026-05: Runtime-failure pass

A scripted pass over every PowerShell code block on the site, prompted by stale snippets surfaced while doing the same audit on the .NET-side gitbook. Each fix below was verified against the freshly-built Visio 4.6.1 module:

* **`technical-notes/use-visioautomation.md`**: the script referenced `Get-VisioScriptingClient` (renamed to `Get-VisioClient`), `$sc.Assemblies` (no such property on `VisioScripting.Client`), `VisioAutomation.Geometry.Point` / `Rectangle` (the geometry primitives moved to `VisioAutomation.Core`), and `VisioAutomation.ShapeSheet.SRCConstants` (renamed to `VisioAutomation.Core.SrcConstants`). Rewritten using the modern type names; the `Add-Type` loop is gone because `Import-Module Visio` already loads the underlying assemblies.
* **`cmdlets/pages/format-visiopage.md`**: the auto-layout example had the same broken `$sc.Assemblies | ForEach-Object { Add-Type -Path $_ }` loop. Removed it; the `New-Object VisioAutomation.Models.LayoutStyles.FlowchartLayoutStyle` call works directly after `Import-Module`.
* **`cmdlets/custom-properties/examples.md`**: the `Write-Host` line dereferenced `$custompropcells.Value.Formula`, but `Value` is a `Core.CellValue` whose underlying property is `.Value`, not `.Formula`. Fixed.
* **`samples/draw-fill-patterns.md`**: `New-VisioShape -Type Rectangle ...` (no `-Type` parameter) replaced with `New-VisioShape -Rectangle (New-VisioRectangle ...)`. Also `-Shapes` (plural) on `Set-VisioText` and `Set-VisioShapeCells` corrected to `-Shape`.
* **`cmdlets/shapes/enumerate-selected-shapes.md`**: the description claimed `Get-VisioShape` with no arguments returned the currently-selected shapes; it actually returns every shape on the active page. Description, syntax block, and examples brought into agreement with `GetVisioShape.cs`.
* **`cmdlets/shapecells/new-visioshapecells.md`**: the prose listed `XFormWidth, PinX` as example properties; `PinX` doesn't exist on `ShapeCells`, the property is `XFormPinX`. Corrected.

## 2026-05: Refresh against module 4.6.1

A large refresh aligning every cmdlet page with the **Visio PowerShell 4.6.1** module released on 2026-05-03. The work touched almost every page.

### New cmdlet pages

Cmdlets that previously had no documentation now have full pages:

* [New-VisioShape](cmdlets/shapes/new-visioshape.md), [Remove-VisioShape](cmdlets/shapes/remove-visioshape.md)
* [New-VisioPageCells](cmdlets/pages/new-visiopagecells.md), [Set-VisioPageCells](cmdlets/pages/set-visiopagecells.md)
* [Get-VisioShapeCells](cmdlets/shapecells/get-visioshapecells.md), [New-VisioShapeCells](cmdlets/shapecells/new-visioshapecells.md)
* [Get-VisioControl](cmdlets/control/get-visiocontrol.md), [New-VisioControl](cmdlets/control/new-visiocontrol.md), [Remove-VisioControl](cmdlets/control/remove-visiocontrol.md): entirely new section
* All seven [VisioApplication cmdlets](cmdlets/visioapplication/) (Close, Get, New, Out, Test, Undo, Redo)
* [Copy-VisioPage](cmdlets/pages/invoke-visioduplicate-page.md), [Select-VisioPage](cmdlets/pages/select-visiopage-tbd.md), [Get-VisioText](cmdlets/text/get-visiotext.md): previously marked `[TBD]`
* [Other cmdlets](cmdlets/other-cmdlets.md): a single page covering the small/utility cmdlets (`Get-VisioClient`, `Get-VisioLockCells`, `Import-VisioModel`, `Measure-VisioShape`, `New-VisioPoint`, `New-VisioRectangle`, `Select-VisioDocument`, `Test-VisioDocument`)

### Standardized layout

Every cmdlet page now follows the same structure:

* A one-sentence intro with the cmdlet name in bold.
* A **Syntax** block in PowerShell `Get-Help -Syntax` style. Cmdlets with multiple parameter sets get one syntax block per set.
* A **Parameters** table with name, type, required-or-not, and description.
* An **Examples** section grouping the per-task examples.
* A **See also** section linking to related cmdlets.

If you used to skim cmdlet pages looking for the parameter list, the `## Parameters` table is now the place to find it.

### Documents new behavior in 4.6.1

The `Lock-VisioShape` / `Unlock-VisioShape` / `Export-VisioShape` / `New-VisioShape` pages reflect bug fixes that shipped in **4.6.1**:

* `Lock-VisioShape` and `Unlock-VisioShape` switches (`-Width`, `-Height`, `-MoveX`, etc.) now actually take effect. In 4.6.0 and earlier, the switches were silently ignored.
* `Export-VisioShape` no longer needs `-Overwrite` to write to a fresh path. The previous "Known limitation" note has been removed.
* `New-VisioShape -Polyline` requires at least 2 points; `-Bezier` requires at least 4. The cmdlet now actually enforces this.

The lock-related pages call out the version requirement explicitly so readers on older modules aren't misled.

### Corrected examples

Many example snippets in the previous docs referenced cmdlets, parameters, or values that don't exist in the module. They've all been corrected:

* `Set-VisioPage` (used throughout the old `Get-VisioPage` page) is not a real cmdlet: references replaced with `Select-VisioPage`.
* `Set-VisioDocument`, `Get-VisioScriptingClient`, `New-VisioGroup`: none of these exist; replaced with the actual cmdlets (`Select-VisioDocument`, `Get-VisioClient`, `Join-VisioShape`).
* `Export-VisioPage -AllPages`: this parameter doesn't exist. Replaced with a `foreach` loop over `Get-VisioPage`.
* `Select-VisioShape All` / `None` / `Invert`: the actual enum values are `SelectAll`, `SelectNone`, `InvertSelection`. PowerShell does not accept the abbreviated forms.
* `Get-VisioShape -Recursive`: this parameter doesn't exist; removed.
* `New-VisioShape -Masters X -Points Y,Z`: the actual parameters are singular `-Master` and `-Position` (and `-Position` takes `Point` objects, not loose numbers). Standardized to `-Master $m -Position (New-VisioPoint X Y)`.
* `Format-VisioShape -NudgeX` for vertical nudges: the vertical equivalent is `-NudgeY`.
* `Format-VisioWindow` parameter names in prose were `-To`, `-Value`, `-ValueRelative`; the actual names are `-ZoomTo`, `-Zoom`, `-ZoomRelative`.
* `New-Object VisioAutomation.Geometry.Point(...)`: the `Geometry` namespace doesn't exist; the actual class is `VisioAutomation.Core.Point`. Examples switched to the idiomatic `New-VisioPoint X Y`.

### Publishing-to-PowerShell-Gallery rewrite

The [Publish to PowerShell Gallery](developer-info/publishing-to-powershell-gallery.md) page was rewritten end-to-end after a real publish exercise surfaced several gotchas (TLS 1.2, in-box PowerShellGet 1.x bugs, PS 5.1 vs 7 module path, `.ps1` file encoding). The page now points at the new `Publish-VisioPSToGallery.ps1` release script and documents both the quick path and the manual fallback.
