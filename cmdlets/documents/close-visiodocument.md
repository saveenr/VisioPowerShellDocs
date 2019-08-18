# Close-VisioDocument

#### NOTE: Unsaved documents will be closed without prompting

To simplify automation, the Close-VisioDocument cmdlet will close any specific document - even if it has unsaved changes.

#### **Close the active document** <a id="closing-a-specific-document"></a>

```text
Close-VisioDocument
```

#### Close a specific document <a id="closing-a-specific-document"></a>

```
Close-VisioDocument -Document $doc1
```

#### Close multiple documents <a id="closing-multiple-documents"></a>

```text
Close-VisioDocument -Document $doc1,$doc2 
```

#### Close all documents <a id="close-all-documents"></a>

```text
$docs = Get-VisioDocument -Name *
Close-VisioDocuments $docs 
```

###  <a id="the-active-document"></a>

