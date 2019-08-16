# Close-VisioDocument

**Closing the active document**

```text
Close-VisioDocument
```

#### Unsaved documents will be closed without prompting <a id="forcing-a-document-to-close"></a>

To simplify automation, the Close-VisioDocument cmdlet will close any specific document - even if it has unsaved changes.

#### Closing a specific document <a id="closing-a-specific-document"></a>

You can specify the document object to close

```text
Close-VisioDocument -Document $doc1
```

#### Closing multiple documents <a id="closing-multiple-documents"></a>

```text
Close-VisioDocument -Document $doc1,$doc2 
```

#### Close all documents <a id="close-all-documents"></a>

```text
$docs = Get-VisioDocument -Name *
Close-VisioDocuments $docs 
```

###  <a id="the-active-document"></a>

