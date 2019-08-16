# Remove-VisioPage

#### Deletes the active page <a id="deletes-the-active-page"></a>

```text
Remove-VisioPage
```

#### Delete specific pages <a id="delete-specific-pages"></a>

```text
$pages = Get-VisioPage

# deletes the first page
Remove-VisioPage $pages[0] 

# deletes the first and fourth page
Remove-VisioPage $pages[0],$pages[3]
```

#### Delete all pages <a id="delete-all-pages"></a>

```text
$pages = Get-VisioPage
Remove-VisioPage $pages
```

#### Delete all pages that have "2" in their name <a id="delete-all-pages-that-have-2-in-their-name"></a>

```text
Get-VisioPage | Remove-VisioPage
```

###  <a id="the-active-page"></a>

