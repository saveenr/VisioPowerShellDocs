# Documents

A Visio **document** is the file you open in Visio: a drawing (`.vsd`, `.vsdx`) or a stencil (`.vss`, `.vssx`, `.vst`, `.vstx`). One Visio application can have multiple documents open at once; one of them is the *active* document, which most cmdlets default to.

* [`Close-VisioDocument`](close-visiodocument.md): close one or more documents.
* [`Get-VisioDocument`](get-visiodocument.md): enumerate open documents (by name, by ID, or just the active one).
* [`New-VisioDocument`](new-visiodocument.md): create a new document, optionally from a template, with stencils preloaded.
* [`Open-VisioDocument`](open-visiodocument.md): open an existing document or stencil from disk.
* [`Save-VisioDocument`](save-visiodocument.md): save a document, with optional Save-As path.

The two related cmdlets [`Select-VisioDocument`](../other-cmdlets.md) (switch which document is active) and [`Test-VisioDocument`](../other-cmdlets.md) (boolean: is any document open?) are documented in the [Other cmdlets](../other-cmdlets.md) note.
