# Detect if VisioPS is installed

```text
Import-Module visio

$module = Get-Module -Name "Visio"
if ($module -eq $null)
{
    Write-Host "VisioPS" not installed
}
else
{
    $modpath = $module.Path
    $modver = $module.Version
    $modfolder = Split-Path $modpath -Parent
    Write-Host VisioPS `($modver`) is installed at `"$modfolder`"
}
```

  


