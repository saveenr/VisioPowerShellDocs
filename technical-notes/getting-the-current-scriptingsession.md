# VisioScriptingClient

Most of the logic in VisioPS is implemented by a layer called **VisioAutomation.Scripting**. There is a **ScriptingClient** object that takes care of most of the hard work of interactively working with Visio.

Get the current **ScriptingClient** object by using the**Get-VisioScriptingClient** cmdlet.

```text
$sc = Get-VisioScriptingClient
```



