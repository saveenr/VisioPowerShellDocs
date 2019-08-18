# Get-VisioDocument

#### Get all documents  <a id="get-all-documents"></a>

```text
Get-VisioDocument -Name *
```

#### Get all documents based on the document name <a id="get-all-documents-based-on-the-document-name"></a>

```text
# To find a specific document with name "DocumentFoo"
Get-VisioDocument -Name "DocumentFoo"
```

#### Get the active document <a id="get-the-active-document"></a>

```text
Get-VisioDocument -ActiveDocument
```

#### Set the Active Document <a id="set-the-active-document"></a>

```text
# using a document object
Set-VisioDocument $doc

# Using the name the document
Set-VisioDocument "Drawing5"
```

#### Checking if the Active Document is valid <a id="checking-is-the-active-document-is-valid"></a>

Sometimes you'll need to perform an action only if a drawing is open. The easy way to check is to use Test-VisioDocument

```text
If (Test-VisioDocument)
{
    # do something
}
else
{
    # do something else
}
```

