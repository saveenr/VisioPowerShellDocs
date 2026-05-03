# Remove-VisioPage

#### Deletes the active page <a href="#deletes-the-active-page" id="deletes-the-active-page"></a>

```
Remove-VisioPage
```

#### Delete specific pages <a href="#delete-specific-pages" id="delete-specific-pages"></a>

```
$pages = Get-VisioPage

# deletes the first page
Remove-VisioPage $pages[0] 

# deletes the first and fourth page
Remove-VisioPage $pages[0],$pages[3]
```

#### Delete all pages <a href="#delete-all-pages" id="delete-all-pages"></a>

```
$pages = Get-VisioPage
Remove-VisioPage $pages
```

#### Delete all pages that have "2" in their name <a href="#delete-all-pages-that-have-2-in-their-name" id="delete-all-pages-that-have-2-in-their-name"></a>

```
Get-VisioPage | Remove-VisioPage
```

### &#x20;<a href="#the-active-page" id="the-active-page"></a>
