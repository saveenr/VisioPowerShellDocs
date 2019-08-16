# Enumerate documents

#### Get all documents <a id="get-all-documents"></a>

```text
$alldocs = Get-VisioDocument
```

#### Get all documents based on the document name <a id="get-all-documents-based-on-the-document-name"></a>

```text

# To find a specific document Get-VisioDocument "DocumentFoo"
Get-VisioDocument "DocumentFoo"

# To find documents with any name
Get-VisioDocument "*"

# Use wildcards. Find all documents with a "3" in their name
$alldocs = Get-VisioDocument "*3*"
```

###  <a id="the-active-document"></a>

