# Close-VisioDocument

The **Close-VisioDocument** cmdlet closes one or more open Visio documents. With no arguments, it closes the active document.

> **Note:** to simplify automation, the cmdlet closes documents **without prompting**, even if they contain unsaved changes. Save first if you don't want to lose work.

## Syntax

```powershell
Close-VisioDocument [-Document <Document[]>]
```

## Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `-Document` | `Document[]` | No | The document or documents to close. If omitted, the active document is closed. |

## Examples

### Close the active document

```powershell
Close-VisioDocument
```

### Close a specific document

```powershell
Close-VisioDocument -Document $doc1
```

### Close multiple documents

```powershell
Close-VisioDocument -Document $doc1,$doc2
```

### Close all open documents

```powershell
$docs = Get-VisioDocument -Name *
Close-VisioDocument -Document $docs
```

## See also

* [Get-VisioDocument](get-visiodocument.md)
* [New-VisioDocument](new-visiodocument.md)
* [Open-VisioDocument](open-visiodocument.md)
* [Save-VisioDocument](save-visiodocument.md)
