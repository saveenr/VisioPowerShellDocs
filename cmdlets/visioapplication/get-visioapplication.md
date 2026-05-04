# Get-VisioApplication

The **Get-VisioApplication** cmdlet returns the Visio application instance currently bound to the PowerShell session, or `$null` if no application is attached.

## Syntax

```powershell
Get-VisioApplication
```

## Parameters

`Get-VisioApplication` takes no parameters.

## Examples

### Get the bound application

```powershell
$app = Get-VisioApplication
$app.Version
```

### Check whether an application is bound

`Test-VisioApplication` is a cleaner way to check and returns a boolean.

```powershell
if (Test-VisioApplication) {
    $app = Get-VisioApplication
    Write-Host "Bound to Visio $($app.Version)"
}
else {
    Write-Host "No Visio application attached"
}
```

## See also

* [New-VisioApplication](new-visioapplication.md)
* [Close-VisioApplication](close-visioapplication.md)
* [Test-VisioApplication](test-visioapplication.md)
