# List cmdlets

To see a list of them use the Get-Command cmdlet as shown below

```text
Get-Command -Module Visio | Select Name
```

The output is ordered by the cmdlet verb. A useful option is to organize by the cmdlet noun as shown below.

```text
Get-Command -Module Visio | Sort-Object Noun,Verb | Select Name
```

Listing just the nouns makes it easier to see the surface area of the VisioPS cmdlets

```text
Get-Command -Module Visio | Sort-Object Noun -Unique | Select Noun
```

