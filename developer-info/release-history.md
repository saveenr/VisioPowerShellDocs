# Release history

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

