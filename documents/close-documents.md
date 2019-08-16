# Close documents

**Closing the active document**

```text
Close-VisioDocument
```

#### Forcing a document to close <a id="forcing-a-document-to-close"></a>

If the document has been modified then Visio won't close the document automatically. Instead it will ask the user to close or not. 

To avoid this prompt and force Visio to close the document use `-Force`.

```text
Close-VisioDocument -Force
```

#### Closing a specific document <a id="closing-a-specific-document"></a>

You can specify the document object to close

```text
Close-VisioDocument -Documents $doc1
```

#### Closing multiple documents <a id="closing-multiple-documents"></a>

```text
Close-VisioDocument -Documents doc1,doc2 -Force
```

#### Close all documents <a id="close-all-documents"></a>

```text
$docs = Get-VisioDocument
Close-VisioDocuments $docs -Force
```

###  <a id="the-active-document"></a>

