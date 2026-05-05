# VisioClient

Most of the cmdlets in this module are thin wrappers over a .NET layer called **`VisioScripting`**, whose entry point is a `Client` object. The cmdlets share a single `Client` instance for the PowerShell session, and you can reach for it directly when you need to call API surface that the cmdlets don't expose.

Get the current `Client` with [`Get-VisioClient`](../cmdlets/other-cmdlets.md):

```powershell
$client = Get-VisioClient
```

From there you can call into any of the `VisioScripting` command groups (`Document`, `Page`, `Selection`, `View`, `Application`, etc.), or its `Client.Application` property to reach the raw `IVisio.Application` COM object.

## See also

* [Use VisioAutomation](use-visioautomation.md): calling into the bundled `VisioAutomation` library directly.
* [`Get-VisioClient`](../cmdlets/other-cmdlets.md): reference (covered in the Other cmdlets note).

> **Historical note.** This cmdlet was called `Get-VisioScriptingClient` in earlier module versions and was renamed to the shorter `Get-VisioClient`. Old scripts referencing the long name need updating.
