# Tips

A handful of small habits that make scripts using this module easier to debug and more reliable.

## Fail fast on errors

If you're new to PowerShell, put these two lines at the top of every script:

```powershell
Set-StrictMode -Version 2
$ErrorActionPreference = "Stop"
```

Strict mode catches typos in variable names and references to undefined properties; the error-action preference makes any cmdlet error stop the script instead of being silently swallowed.

## Add `-Verbose` while iterating

When something doesn't behave the way you expect, append `-Verbose` to the suspect cmdlet to see what it's actually doing. See [Verbose logging](verbose-logging.md).

## Use `Get-Help` for cmdlet syntax

`Get-Help <cmdlet> -Syntax` is the fastest way to recall the parameter signature. See [Get help for a cmdlet](get-help-for-a-cmdlet.md).

## Watch out for the active-thing defaults

Most cmdlets default to "the active document / page / selection" when their `-Document` / `-Page` / `-Shape` parameters are omitted. That's convenient for quick scripts but bites scripts that expect a specific target &mdash; pass the parameter explicitly when correctness matters. See [Context-sensitivity](context-sensitivity.md).
