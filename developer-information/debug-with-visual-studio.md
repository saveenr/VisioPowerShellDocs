# Debug with Visual Studio



### Using the Visual Studio Debugger <a href="#using-the-visual-studio-debugger" id="using-the-visual-studio-debugger"></a>

In the Solution Explorer right-click on VisioPowerShell project and select **Properties**.

**Navigate to Debug**

For **Start action** set **Start external program** to one of the following

```
c:\windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

For **Start options**, set **Command line arguments** to:

```
-NoProfile -NoExit -Command "Import-Module .\Visio.psd1"
```

For using PowerShell ISE

```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell_ise.exe
```

And command line options

```
-NoProfile
```
