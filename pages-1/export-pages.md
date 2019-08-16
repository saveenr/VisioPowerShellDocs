# Export pages

#### Export a page as an image <a id="export-a-page-as-an-image"></a>

```text
Export-VisioPage "d:\foo.png"
```

#### Export each page to separate Image <a id="export-each-page-to-separate-image"></a>

```text
Export-VisioPage "d:\foo.png" -AllPages
```

Will create a PNG for each page. The name will be of the form `foo_Page_N.png`

