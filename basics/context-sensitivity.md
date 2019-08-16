# Context-sensitivity

### Introduction

For most VisioPS cmdlets you never need to identify the target of the operation.

For example, the `Set-VisioText` cmdlet works against the selected shapes in the active document. If no shapes are selected, then nothing happens. 

```text
Set-VisioText -Text "Hello World"
```

The ability for cmdlets to target the appropriate objects based on context dramatically simplifies automating Visio with VisioPS. 

### Overriding context sensitivity

Sometimes its more convenient to explicitly identify the targets of a cmdlet. Depending on the cmdlet, the following parameters will be available:

* `-Documents`
* `-Pages`
* `-Shapes`



