# Active document

#### Get the active document <a href="#get-the-active-document" id="get-the-active-document"></a>

```
Get-VisioDocument -ActiveDocument
```

#### Set the Active Document <a href="#set-the-active-document" id="set-the-active-document"></a>

```
# using a document object
Set-VisioDocument $doc

# Using the name the document
Set-VisioDocument "Drawing5"
```

#### Checking is the Active Document is valid <a href="#checking-is-the-active-document-is-valid" id="checking-is-the-active-document-is-valid"></a>

Sometimes you'll need to perform an action only if a drawing is open. The easy way to check is to use Test-VisioDocument

```
If (Test-VisioDocument)
{
    # do something
}
else
{
    # do something else
}
```
