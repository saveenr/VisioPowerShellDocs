# Test-VisioShape

The `Test-VisioShape` cmdlet returns `$true` if anything is currently selected on the active page, `$false` otherwise. It is a thin convenience over checking the selection size and is useful as a guard before running selection-dependent cmdlets.

`Test-VisioShape` takes no parameters.

### Branch on whether anything is selected

```powershell
if (Test-VisioShape) {
    Format-VisioShape -AlignHorizontal Center
}
else {
    Write-Host "Nothing selected — skipping"
}
```

### See also

* [Select-VisioShape](selecting-shapes.md) &mdash; change the selection.
* [Get-VisioShape](selecting-shapes.md) &mdash; read the current selection.
