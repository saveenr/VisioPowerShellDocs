# Visio version compatibility

## Supported Visio versions

The module works with **Visio 2010 and later**, including modern Microsoft 365 / Visio Plan 2 builds. Internally the module is built against the Visio 2010 PIA (Primary Interop Assembly) for maximum back-compatibility; APIs added since 2010 are not exposed through the module's typed surface but are reachable via the underlying `IVisio` objects when needed.

## Bitness (32-bit vs 64-bit)

The module supports both 32-bit and 64-bit Visio installs. The PowerShell process that imports the module must match the Visio bitness, since COM activation goes through an in-process bridge. If you have 64-bit Visio installed, run the module from 64-bit PowerShell; for 32-bit Visio, run from 32-bit PowerShell (`powershell.exe` from `SysWOW64` on a 64-bit Windows).

## See also

* [PowerShell version compatibility](../powershell/powershell-version-compatibility.md)
