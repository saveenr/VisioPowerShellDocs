# Get-VisioPage

### Enumerate all pages from the active document

```text
$pages = Get-VisioPage
```

#### Enumerate all pages from the active document that have a specific name <a id="get-all-pages-from-active-document-that-have-a-specific-name"></a>

```text
$pages = Get-VisioPage "Page-1"
```

#### Enumerate all pages from the active document using wildcards <a id="using-wildcards"></a>

```text
$pages = Get-VisioPage "*foo"
```

#### Get the active page <a id="get-the-active-page-from-the-active-document"></a>

```text
$page = Get-VisioPage -ActivePage
```

### Set the active page

```text
# By name
Set-VisioPage -Name "Mypage"

# Using a reference to a specific page
Set-VisioPage -Page $p
```

### Set a new active page relative to the current active page <a id="set-the-active-page-relative-to-the-active-page"></a>

```text
Set-VisioPage -Direction First
Set-VisioPage -Direction Last
Set-VisioPage -Direction Next
Set-VisioPage -Direction Previous
```

