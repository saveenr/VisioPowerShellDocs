# Release history

**Version 5.1.0** (2026/11/20) `Out-VisioApplication` gains a `-DirectedGraphStyling` parameter to choose the connector master for a directed graph, and `-OrgChart` no longer needs an open document: it needs only an attached Visio application. The module bundles VisioAutomation 5.0.0, which removes the Box layout, the form page model and `client.Developer` and renames the `client.Model` draw methods; no cmdlet is removed or renamed. Full notes are in the [5.1.0 changelog](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md#510---2026-11-20).

**Version 5.0.0** (2026/11/01) The minimum .NET Framework runtime is now 4.7.2 (was 4.5.2), which is built in to Windows 10 version 1809 and Windows Server 2019 and later. Validation failures in `New-VisioShape`, `Export-VisioShape`, `Import-VisioModel`, `Out-VisioApplication`, `New-VisioPage`, `Set-VisioCustomProperty`, `Get-VisioPageCells` and `Get-VisioShapeCells` now stop the cmdlet regardless of `$ErrorActionPreference`, and carry a stable `FullyQualifiedErrorId`. Bundles VisioAutomation 4.0.0. Details are in the [module changelog](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md).

**Version 4.8.0** (2026/10/01) Adds `Get-VisioPage -Index` for positions in the document. `Get-VisioPage -ID` is now a real Visio page ID (use `-Index` for positions), and `New-VisioDocument -Template` creates the document from the template. Fixes `Format-VisioPage -Width` / `-Height` and the boolean and sort-key parameters of `New-VisioHyperlink`. Bundles VisioAutomation 3.2.0. Versions 4.7.0 to 4.7.3 are described in the [module changelog](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md).

**Version 4.6.1** (2026/05/03) First release from the 2026 refresh. Bug fixes: `Lock-VisioShape` / `Unlock-VisioShape` switches now actually bind (were silently ignored); `Export-VisioShape` no longer trips on its inverted file-existence check; `New-VisioShape` polyline / Bezier minimum-point validation actually throws. Bundled DLLs target .NET Framework 4.5.2 (was 4.5). See [`CHANGELOG.md`](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md) for the full list.

**Version 4.4.0** (2021/11/22) Added cmdlets to simplify creation of Geometric primitives

**Version 4.0.0** (2019/08/14) This version is a major cleanup of how the cmdlets work to make them more consistent and reliable. It breaks backward compatibility with the 3.x versions.

**Version 3.0.1** (2019/03/09) Updated package metadata

**Version 3.0.0** (2019/03/09) Major cmdlet refactoring

**Version 1.2.211** Bugfix

**Version 1.2.210** Bugfix to Set-VisioPageCell and Set-VisioShapeCell&#x20;

**Version 1.2.209** Maintenance release

**Version 1.1.25** Bugfix - when retrieving Custom Properties

**Version 1.1.23** Bugfix - was dividing by zero when operations were done on zero shapes

**Version 1.1.14** Bugfix - that presented Custom Properties from being retrieved correctly

**Version 1.1.11** Perf improvement -  increased performance when working with ShapeSheet

