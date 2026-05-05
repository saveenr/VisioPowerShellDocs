# Create a new Visio application COM object

`New-VisioApplication` is the supported way to start Visio from the module: it starts the application **and** binds the PowerShell session to it so subsequent cmdlets target the right instance.

```powershell
New-VisioApplication
```

If you need the raw COM object directly (e.g. for advanced interop scenarios that the module doesn't cover), the equivalent without going through the module is:

```powershell
$application = New-Object -ComObject Visio.Application
```

This bypasses the session-binding and verbose-logging that `New-VisioApplication` does, so most users should prefer the cmdlet.

## See also

* [`New-VisioApplication`](../../cmdlets/visioapplication/new-visioapplication.md)
* [`Get-VisioClient`](../getting-the-current-scriptingsession.md): drop down further to the `VisioScripting.Client` for .NET-side interop.
