# Test-VisioApplication

The **Test-VisioApplication** cmdlet returns `$true` if the PowerShell session is bound to a running Visio application, `$false` otherwise. Useful as a guard before invoking cmdlets that require an attached application.

## Syntax

```powershell
Test-VisioApplication
```

## Parameters

`Test-VisioApplication` takes no parameters.

## Examples

### Branch on whether a Visio application is attached

```powershell
if (-not (Test-VisioApplication)) {
    New-VisioApplication
}
```

### Verify before running selection-dependent cmdlets

```powershell
if (Test-VisioApplication) {
    Set-VisioText "Hello"
}
else {
    Write-Host "No Visio app -- nothing to do"
}
```

## See also

* [New-VisioApplication](new-visioapplication.md)
* [Get-VisioApplication](get-visioapplication.md)
* [Test-VisioDocument](../documents/get-visiodocument.md): check whether a document is open within the application.
