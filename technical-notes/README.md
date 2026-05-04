# Technical notes

Background and reference material for advanced or unusual scenarios &mdash; version compatibility, low-level interop, and how the module bridges to the underlying VisioAutomation .NET library.

## Visio

* [Visio version compatibility](visio/README.md) &mdash; which Visio versions the module supports.

## PowerShell

* [PowerShell compatibility](powershell/README.md) &mdash; which PowerShell editions and versions the module supports, plus how to install or detect them.

## Bridges to the .NET library

* [VisioClient](getting-the-current-scriptingsession.md) &mdash; obtain the underlying `VisioScripting.Client` object when you need to drop down to the .NET API directly.
* [Use VisioAutomation](use-visioautomation.md) &mdash; calling into the bundled VisioAutomation library from PowerShell.
