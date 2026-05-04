# New-VisioApplication

The **New-VisioApplication** cmdlet starts a new Visio application instance and binds the PowerShell session to it. Subsequent cmdlets that operate on "the active application" use this instance.

The cmdlet does not write the application object to the pipeline (intentional &mdash; returning it has historically caused Visio to error on shutdown). Use [Get-VisioApplication](get-visioapplication.md) afterward if you need a handle.

## Syntax

```powershell
New-VisioApplication
```

## Parameters

`New-VisioApplication` takes no parameters.

## Examples

### Start a Visio application

```powershell
Import-Module Visio

New-VisioApplication
New-VisioDocument
```

### Capture the application instance

```powershell
New-VisioApplication
$app = Get-VisioApplication
```

## See also

* [Get-VisioApplication](get-visioapplication.md)
* [Close-VisioApplication](close-visioapplication.md)
* [Test-VisioApplication](test-visioapplication.md)
