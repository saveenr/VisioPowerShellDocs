# Close-VisioDocument

#### NOTE: Unsaved documents will be closed without prompting

To simplify automation, the Close-VisioDocument cmdlet will close any specific document - even if it has unsaved changes.

#### **Close the active document** <a href="#closing-a-specific-document" id="closing-a-specific-document"></a>

```
Close-VisioDocument
```

#### Close a specific document <a href="#closing-a-specific-document" id="closing-a-specific-document"></a>

```
Close-VisioDocument -Document $doc1
```

#### Close multiple documents <a href="#closing-multiple-documents" id="closing-multiple-documents"></a>

```
Close-VisioDocument -Document $doc1,$doc2 
```

#### Close all documents <a href="#close-all-documents" id="close-all-documents"></a>

```
$docs = Get-VisioDocument -Name *
Close-VisioDocuments $docs 
```

### &#x20;<a href="#the-active-document" id="the-active-document"></a>
