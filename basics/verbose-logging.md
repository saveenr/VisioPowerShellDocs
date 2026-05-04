# Verbose logging

If you're having trouble with a cmdlet, add `-Verbose`. Most cmdlets in the module emit additional diagnostic output that explains what they're targeting and what they did.

```powershell
New-VisioApplication -Verbose
Set-VisioText "Hello" -Verbose
```

`-Verbose` is a built-in PowerShell common parameter and works on every cmdlet, even ones that don't define their own verbose messages.

To force verbose output for a whole script (rather than per call), set the preference variable at the top:

```powershell
$VerbosePreference = "Continue"
```
