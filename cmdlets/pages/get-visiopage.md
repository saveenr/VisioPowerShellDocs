# Get-VisioPage

### Enumerate all pages from the active document

```
$pages = Get-VisioPage
```

#### Enumerate all pages from the active document that have a specific name <a href="#get-all-pages-from-active-document-that-have-a-specific-name" id="get-all-pages-from-active-document-that-have-a-specific-name"></a>

```
$pages = Get-VisioPage "Page-1"
```

#### Enumerate all pages from the active document using wildcards <a href="#using-wildcards" id="using-wildcards"></a>

```
$pages = Get-VisioPage "*foo"
```

#### Get the active page <a href="#get-the-active-page-from-the-active-document" id="get-the-active-page-from-the-active-document"></a>

```
$page = Get-VisioPage -ActivePage
```

### Set the active page

```
# By name
Set-VisioPage -Name "Mypage"

# Using a reference to a specific page
Set-VisioPage -Page $p
```

### Set a new active page relative to the current active page <a href="#set-the-active-page-relative-to-the-active-page" id="set-the-active-page-relative-to-the-active-page"></a>

```
Set-VisioPage -Direction First
Set-VisioPage -Direction Last
Set-VisioPage -Direction Next
Set-VisioPage -Direction Previous
```
