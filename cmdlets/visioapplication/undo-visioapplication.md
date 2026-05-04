# Undo-VisioApplication

The **Undo-VisioApplication** cmdlet undoes the last action in the bound Visio application &mdash; the same operation as `Ctrl+Z` in the Visio UI.

## Syntax

```powershell
Undo-VisioApplication
```

## Parameters

`Undo-VisioApplication` takes no parameters.

## Examples

### Undo the last action

```powershell
Undo-VisioApplication
```

### Undo several steps

```powershell
1..5 | ForEach-Object { Undo-VisioApplication }
```

## See also

* [Redo-VisioApplication](redo-visioapplication.md)
