# Close-VisioApplication

The **Close-VisioApplication** cmdlet shuts down the Visio application instance currently bound to the PowerShell session.

> **Note:** open documents are closed without prompting, even if they have unsaved changes. Save first if you need to keep the work; see [Save-VisioDocument](../documents/save-visiodocument.md).

## Syntax

```powershell
Close-VisioApplication
```

## Parameters

`Close-VisioApplication` takes no parameters.

## Examples

### Close the bound application

```powershell
Close-VisioApplication
```

### Save then close

```powershell
foreach ($doc in Get-VisioDocument -Name *) {
    Save-VisioDocument -Document $doc
}
Close-VisioApplication
```

## See also

* [New-VisioApplication](new-visioapplication.md)
* [Get-VisioApplication](get-visioapplication.md)
* [Save-VisioDocument](../documents/save-visiodocument.md)
* [Close-VisioDocument](../documents/close-visiodocument.md): close individual documents without exiting Visio.
