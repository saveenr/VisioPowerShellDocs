# Master

A **master** is a reusable shape definition stored in a stencil. When you drop a master onto a page with [`New-VisioShape -Master`](../shapes/new-visioshape.md), Visio creates an instance of that master on the page.

* [`Get-VisioMaster`](get-visiomaster.md) &mdash; look up masters in a document by name, or enumerate all of them.

Open a stencil with [`Open-VisioDocument`](../documents/open-visiodocument.md) before calling `Get-VisioMaster` &mdash; stencils are documents in their own right.
