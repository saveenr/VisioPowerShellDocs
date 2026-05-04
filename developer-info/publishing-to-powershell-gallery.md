# Publish to PowerShell Gallery

The Visio module ships from [https://www.powershellgallery.com/packages/Visio/](https://www.powershellgallery.com/packages/Visio/).

## Quick path (recommended)

The repo includes a release script that handles every step end-to-end:

```powershell
$env:PSGalleryApiKey = '<your API key>'
& '<repo>\VisioAutomation_2010\VisioPowerShell\Publish-VisioPSToGallery.ps1'
```

The script:

1. Verifies the running PowerShell host is at least 5.1 (Publish-Module's floor) and prints what's running.
2. Forces TLS 1.2 (PSGallery rejects anything older).
3. Reads `ModuleVersion` from `Visio.psd1`.
4. Stages the Debug build into the user-modules folder via `InstallForCurrentUser.ps1`, then verifies the staged manifest version matches the source version (catches stale-build mismatches).
5. Calls `Publish-Module -Path` (not `-Name`, to avoid the PS 5.1 vs 7 module-path divergence).
6. Polls PSGallery for up to 30 seconds to verify the new version is actually live.
7. Only then tags `HEAD` as `VisioPS_<version>` and pushes the tag.

The script refuses to tag a dirty working tree, a branch that's out of sync with origin, or a version already tagged. Use `-WhatIf` for a dry run that skips publish and tagging.

## One-time prerequisites

These setup steps only need to be done once per dev machine:

### 1. Be the package owner

You must be listed as an owner of the `Visio` package on PSGallery. New owners are added via the [package-management page](https://www.powershellgallery.com/packages/Visio/Owners) by an existing owner.

### 2. Generate an API key

Log in to [https://www.powershellgallery.com/account/apikeys](https://www.powershellgallery.com/account/apikeys) and create a key scoped to `Push new packages and package versions` for `Visio`. Treat it like a password &mdash; rotate it if it ever leaks into a transcript or a screenshot.

### 3. Upgrade PowerShellGet (Windows PowerShell 5.1 only)

Windows ships with `PowerShellGet 1.0.0.1`, which has a bug that swallows `Publish-Module` failures and reports them as success. Upgrade to a current version:

```powershell
Install-Module PowerShellGet -Force -Scope CurrentUser -AllowClobber
```

The `-AllowClobber` flag is required because the upgrade pulls in a newer `PackageManagement` whose cmdlet names overlap with the in-box version.

**Close and reopen your PowerShell session after the upgrade** &mdash; the running session has the old PowerShellGet still loaded.

PowerShell 7 ships with a current PowerShellGet, so this step doesn't apply there.

### 4. Build the solution in Debug

The release script reads from `bin/Debug`, so build the solution before staging:

```bash
MSBUILD="/c/Program Files/Microsoft Visual Studio/2022/Community/MSBuild/Current/Bin/MSBuild.exe"
"$MSBUILD" VisioAutomation_2010/VisioAutomation2010.sln -t:Restore -p:RestorePackagesConfig=true
"$MSBUILD" VisioAutomation_2010/VisioAutomation2010.sln -p:Configuration=Debug -m
```

If you bump the version in `Visio.psd1`, **rebuild before publishing** &mdash; otherwise the staged module ships with the old version. The release script catches this case and refuses to publish, but rebuilding upfront avoids the round-trip.

## Gotchas we've hit

The release script handles all of these, but they're documented here so the workarounds are findable when something new breaks.

| Symptom | Cause | Resolution |
| --- | --- | --- |
| `Could not create SSL/TLS secure channel` from `Publish-Module`. | PS 5.1 defaults to TLS 1.0/1.1 in many configs; PSGallery requires 1.2. | Script sets `[Net.ServicePointManager]::SecurityProtocol` to include `Tls12` at startup. |
| Script reports success ("Done.") but the version is missing from PSGallery. | PowerShellGet 1.x catches its own internal `Write-Error` calls and re-emits them as non-terminating, so the outer script can't see the failure. | Upgrade PowerShellGet (see prereqs). The script also calls `Publish-Module -ErrorAction Stop` and verifies post-publish via `Find-Module`. |
| `The specified module 'Visio' was not published because no module with that name was found in any module directory.` | Running under PowerShell 7, but `InstallForCurrentUser.ps1` stages to PS 5.1's user-module path (`Documents\WindowsPowerShell\Modules`); PS 7 looks under `Documents\PowerShell\Modules`. | Script uses `Publish-Module -Path` with the explicit staged folder, bypassing module discovery. |
| Parser error like `Unexpected token 'â€”'` on PS 5.1. | `.ps1` script contains non-ASCII characters and lacks a UTF-8 BOM; PS 5.1 reads it using the system code page (Windows-1252) and misdecodes the bytes. | Keep release scripts pure ASCII. |
| `Install-Module PowerShellGet` fails with `commands are already available on this system`. | Newer `PackageManagement` ships paired with the upgraded PowerShellGet and has cmdlet names that collide with the in-box version. | Add `-AllowClobber`. |

## Manual fallback

If the release script breaks for an unrelated reason, you can do the steps by hand:

```powershell
# 1. Force TLS 1.2 (PS 5.1 only)
[Net.ServicePointManager]::SecurityProtocol =
    [Net.ServicePointManager]::SecurityProtocol -bor [Net.SecurityProtocolType]::Tls12

# 2. Stage the build
& '<repo>\VisioAutomation_2010\VisioPowerShell\InstallForCurrentUser.ps1'

# 3. Publish (use -Path, not -Name)
$staged = Join-Path $home 'Documents\WindowsPowerShell\Modules\Visio'
Publish-Module -Path $staged -NuGetApiKey '<your key>' -ErrorAction Stop

# 4. Verify
Find-Module -Name Visio -RequiredVersion '<the version>' -Repository PSGallery

# 5. Tag and push
git tag "VisioPS_<the version>"
git push origin "VisioPS_<the version>"
```

## Tag convention

Each release is tagged on the commit that bumps `Visio.psd1`'s `ModuleVersion`. Tag format:

```
VisioPS_<MAJOR>.<MINOR>.<PATCH>
```

For example, the 4.6.1 release is tagged `VisioPS_4.6.1`. This pattern parallels the existing `VisioAutomation_<version>` tags used for the .NET library, with a different prefix to disambiguate.

## What the script does NOT do

- It does not bump the version in `Visio.psd1` &mdash; do that manually as part of the release commit, alongside the corresponding `[Unreleased]` &rarr; `[<version>]` move in [`VisioPowerShell/CHANGELOG.md`](https://github.com/saveenr/VisioAutomation/blob/master/VisioAutomation_2010/VisioPowerShell/CHANGELOG.md).
- It does not build the solution &mdash; that's still a separate MSBuild invocation.
- It does not publish the NuGet package &mdash; the .NET library has its own (currently manual) release process.
- It does not sign the module DLLs &mdash; signing is a Phase 3 backlog item.
