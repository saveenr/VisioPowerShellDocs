# Export-VisioPage

#### Export a page as an image <a href="#export-a-page-as-an-image" id="export-a-page-as-an-image"></a>

```
Export-VisioPage "d:\foo.png"
```

#### Export each page to separate Image <a href="#export-each-page-to-separate-image" id="export-each-page-to-separate-image"></a>

```
Export-VisioPage "d:\foo.png" -AllPages
```

Will create a PNG for each page. The name will be of the form `foo_Page_N.png`
