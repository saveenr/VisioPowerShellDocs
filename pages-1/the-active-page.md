# The active page

### Get the active page

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

