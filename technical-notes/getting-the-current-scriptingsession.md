# VisioClient

Most of the logic in VisioPS is implemented by a layer called **VisioAutomation.Scripting**. There is a  **Client** object that takes care of most of the hard work of interactively working with Visio.

Get the current **Client** object by using the **Get-VisioClient** cmdlet.

```
$sc = Get-VisioClient
```

In older versions this cmdlet used to be called **Get-VisioSctiptingClient**

