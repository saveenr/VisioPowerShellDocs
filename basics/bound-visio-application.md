# Bound Visio application

When you use VisioPS there cmdlets it typically needs an active instance of Visio to be running - this is called the **bound Visio application**.

#### Bind to a new Visio application <a id="creating-an-binding-to-a-new-visio-application"></a>

```text
New-VisioApplication
```

Note that `New-VisioApplication` does NOT return an application object.

#### Getting the currently bound Visio application <a id="getting-the-bound-application-instance"></a>

```text
$visapp = Get-VisioApplication
```

#### Broken binding <a id="a-bound-visio-instance-may-be-invalid"></a>

Suppose you have a bound instance and then you go to the that instance in the UI and close the application. VisioPS still thinks it bound to that instance - it still "has a pointer" to it. But of course, that pointer is now invalid and any commands that try to interact with the \(now non-existent\) Visio application will fail.

#### Verifying the bound Visio application <a id="a-bound-visio-instance-may-be-invalid"></a>

Use `Test-VisioApplication` to verify that a Visio application instance is bound ans that VisioPS can successfully communicate with it.

```text
if (Test-VisioApplication)
{
    # the bound application is valid
}
else
{
    # the bound application is not valid
}
```

