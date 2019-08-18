# Documents

  
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

# Get-VisioDocument

#### Get all documents  <a id="get-all-documents"></a>

```text
Get-VisioDocument -Name *
```

#### Get the active document

```text
Get-VisioDocument -ActiveDocument
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

#### Checking is the Active Document is valid <a id="checking-is-the-active-document-is-valid"></a>

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

# New-VisioDocument

#### Creating a new empty document <a id="creating-a-new-document"></a>

```text
$d = New-VisioDocument
```

NOTE: The cmdlet will create a new Visio Application object if one is not needed

# Open-VisioDocument

#### Load a document <a id="load-a-document"></a>

```text
Open-VisioDocument "d:\foo.vsd"
```
# Save-VisioDocument

#### Save <a id="save"></a>

```text
Save-VisioDocument
```

#### Save as <a id="save-as"></a>

```text
Save-VisioDocument "d:\foo.vsd"
```

###  <a id="the-active-document"></a>

