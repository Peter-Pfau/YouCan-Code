# Code Snippets
## YouCan-Code
### HostName
```PowerShell
$DNShostname = [System.Net.Dns]::GetHostByName(($env:computerName))
$hostname = $DNShostname.Hostname
$env:username
```
