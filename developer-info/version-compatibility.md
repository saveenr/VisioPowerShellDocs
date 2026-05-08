# Version compatibility

Per-release reference table for the [`Visio`](https://www.powershellgallery.com/packages/Visio) PowerShell module, mapping each version to the PowerShell editions it supports, the .NET runtime its bundled DLLs target, and the contemporaneous [`VisioAutomation2010`](https://www.nuget.org/packages/VisioAutomation2010/) NuGet release that ships inside the module. Use it to pick the right module version for a given environment, or to confirm whether an older module will load into a constrained PowerShell host.

For the matching .NET-side per-version matrix see the [VisioAutomation NuGet version compatibility](https://saveenr.gitbook.io/visioautomation/version-compatibility) page.

## Modern era (changelog-tracked)

These versions are documented in [`VisioPowerShell/CHANGELOG.md`](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md). Every row's data is sourced from the corresponding git tag's `Visio.psd1` and `csproj`.

| Module version | Released | PowerShell host | Bundled DLL TFM | Visio PIA baseline | Bundled VisioAutomation2010 | Release notes |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `4.7.2` | 2026-05-06 | Windows PowerShell 5.1; PowerShell 7+ via the [Windows PowerShell compatibility shim](https://learn.microsoft.com/powershell/scripting/whats-new/module-compatibility) | `net452` | Visio 2010 PIA (v14) | `3.0.0` (matching commit) | [4.7.2 changelog](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md#472---2026-05-06) |
| `4.7.0` | 2026-05-06 | Windows PowerShell 5.1; PowerShell 7+ via the compatibility shim | `net452` | Visio 2010 PIA (v14) | `3.0.0` (matching commit) | [4.7.0 changelog](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md#470---2026-05-06) |
| `4.6.1` | 2026-05-03 | Windows PowerShell 5.1; PowerShell 7+ via the compatibility shim | `net452` | Visio 2010 PIA (v14) | `2.6.0` (matching commit; tag only, not on nuget.org) | [4.6.1 changelog](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md#461---2026-05-03) |

`4.7.2` is the current published release on [PSGallery](https://www.powershellgallery.com/packages/Visio).

### About the `Visio.psd1` `PowerShellVersion = '2.0'` claim

The module's manifest historically declares `PowerShellVersion = '2.0'` and `CLRVersion = '4.0'`. These declarations predate the move to `net452` binaries and are not accurate for the modern releases. The actual minimum is **PowerShell 5.1 on .NET Framework 4.5.2**, because that is what the bundled `VisioPS.dll` and its dependencies require to load. Older PowerShell hosts will fail at module-import time with an assembly-load error. Updating the manifest declarations is tracked separately and does not change the runtime requirements.

## Pre-changelog era

Versions prior to `4.6.1` predate [`VisioPowerShell/CHANGELOG.md`](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md). The data below is reconstructed from the [release-history page](release-history.md) and from inspecting historical commits; runtime details for these versions are best-effort.

| Module version | Released | Notes |
| :--- | :--- | :--- |
| `4.4.0` | 2021-11-22 | Added cmdlets for geometric primitives. |
| `4.0.0` | 2019-08-14 | Major cmdlet refactor; back-compat-breaking with the 3.x line. |
| `3.0.1` | 2019-03-09 | Package metadata update. |
| `3.0.0` | 2019-03-09 | Major cmdlet refactor. |
| `1.x` series (`1.1.11` through `1.2.211`) | various, pre-2019 | Bug fixes and small enhancements. Built against the older `net40` library. |

For the exact set of tags and their dates see the repo's [release tags](https://github.com/saveenr/VisioAutomation/releases) and [git history](https://github.com/saveenr/VisioAutomation/commits/master/).

## Constants across all versions

* **Visio version baseline** is **Visio 2010** (PIA major version 14). The bundled library's typed surface targets the 2010 PIA so it loads cleanly on any Visio install from 2010 onward; APIs added in later Visio versions are reachable through the underlying `IVisio` COM objects but are not surfaced as typed cmdlet parameters.
* **Bitness:** the bundled DLLs are AnyCPU. The PowerShell process that imports the module must match Visio's bitness, since COM activation goes through an in-process bridge. See [Visio version compatibility](../technical-notes/visio/README.md) for details.
* **License:** MIT. Records the `SevenPens` publishing identity from `4.7.0` onward (was `Saveen Reddy` on earlier releases); the license terms themselves are unchanged.

## Future TFM moves

The bundled libraries' minimum target framework will rise from `net452` to `net472` once Windows 10 LTSB 2016 leaves Extended Support on **2026-10-13**. The change will surface in a future module release as a higher .NET Framework requirement on the host. Modern Windows installs already have `net472` available, so the practical impact is on locked-down enterprise images.

## See also

* [VisioAutomation NuGet version compatibility](https://saveenr.gitbook.io/visioautomation/version-compatibility) (the matching matrix for the .NET library)
* [Release history](release-history.md) (per-version release notes for the PowerShell module)
* [Visio version compatibility](../technical-notes/visio/version-compatibility.md) (which Visio versions the module supports, independent of module version)
* [PowerShell version compatibility](../technical-notes/powershell/powershell-version-compatibility.md) (PowerShell host considerations)
* [`Visio` on PowerShell Gallery](https://www.powershellgallery.com/packages/Visio) (current published versions)
