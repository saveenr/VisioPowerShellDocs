# Hyperlinks

A Visio shape can carry one or more **hyperlinks**: targets that the user can navigate to from the shape (URLs, file paths, or sub-addresses such as a specific page or bookmark). Each hyperlink has fields for `Address`, `SubAddress`, `Description`, `Frame`, `SortKey`, `NewWindow`, `Default`, `Invisible`, and `ExtraInfo`.

* [`Get-VisioHyperlink`](get-visiohyperlink.md): read the hyperlinks attached to one or more shapes.
* [`New-VisioHyperlink`](new-visiohyperlink.md): attach a new hyperlink to one or more shapes.
* [`Remove-VisioHyperlink`](remove-visiohyperlink.md): delete a hyperlink by index.

## On the C# side

These cmdlets wrap the [`client.Hyperlink`](https://saveenr.gitbook.io/visioautomation/visio-scripting/hyperlink) command group on the VisioAutomation gitbook. See [VisioScripting.Client](https://saveenr.gitbook.io/visioautomation/visio-scripting) for the full facade index.
