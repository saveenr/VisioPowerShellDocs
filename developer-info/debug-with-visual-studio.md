# Debug with Visual Studio

### Using the Visual Studio Debugger <a id="using-the-visual-studio-debugger"></a>

In the **Solution Explorer**, right-click on the VisioPowerShell project, then select **Properties**.

**Navigate to Debug**

For **Start action** set **Start external program** to one of the following

```text
c:\windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

For **Start options**, set **Command line arguments** to:

```
-NoProfile -NoExit -Command "Import-Module .\Visio.psd1"
```

For using PowerShell ISE

```text
C:\Windows\System32\WindowsPowerShell\v1.0\powershell_ise.exe
```

And command line options

```text
-NoProfile
```

