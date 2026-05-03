# Close documents

**Closing the active document**

```
Close-VisioDocument
```

#### Forcing a document to close <a href="#forcing-a-document-to-close" id="forcing-a-document-to-close"></a>

If the document has been modified then Visio won't close the document automatically. Instead it will ask the user to close or not.&#x20;

To avoid this prompt and force Visio to close the document use `-Force`.

```
Close-VisioDocument -Force
```

#### Closing a specific document <a href="#closing-a-specific-document" id="closing-a-specific-document"></a>

You can specify the document object to close

```
Close-VisioDocument -Documents $doc1
```

#### Closing multiple documents <a href="#closing-multiple-documents" id="closing-multiple-documents"></a>

```
Close-VisioDocument -Documents doc1,doc2 -Force
```

#### Close all documents <a href="#close-all-documents" id="close-all-documents"></a>

```
$docs = Get-VisioDocument
Close-VisioDocuments $docs -Force
```

### &#x20;<a href="#the-active-document" id="the-active-document"></a>
