# Enumerate documents

#### Get all documents <a href="#get-all-documents" id="get-all-documents"></a>

```
$alldocs = Get-VisioDocument
```

#### Get all documents based on the document name <a href="#get-all-documents-based-on-the-document-name" id="get-all-documents-based-on-the-document-name"></a>

```

# To find a specific document Get-VisioDocument "DocumentFoo"
Get-VisioDocument "DocumentFoo"

# To find documents with any name
Get-VisioDocument "*"

# Use wildcards. Find all documents with a "3" in their name
$alldocs = Get-VisioDocument "*3*"
```

### &#x20;<a href="#the-active-document" id="the-active-document"></a>
