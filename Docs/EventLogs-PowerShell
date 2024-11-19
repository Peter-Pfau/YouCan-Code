## Licensing Events

```PowerShell

$DayAgo = (Get-Date) - (New-TimeSpan -hour 24)

$HourAgo = (Get-Date) - (New-TimeSpan -hour 1)

$ComputerName = ""

$Events = get-WinEvent -computername $ComputerName -LogName "Microsoft-Windows-TerminalServices-Licensing/Operational" -MaxEvents 1500 | where-object {$_.TimeCreated -ge $DayAgo}

```

 
## KMS
```PowerShell

$MaxEvents = 200

$Day = 1440

$Hour = 60

$EventAgeMinutes = $Hour

$ComputerName =" "

$KMSMinutesAgo = (icm $ComputerName {Get-Date}) - (New-TimeSpan -minute $EventAgeMinutes)

get-WinEvent -computername $ComputerName -LogName "Key Management Service" -MaxEvents $MaxEvents | where-object {($_.TimeCreated -ge $KMSMinutesAgo)}
 

# Today's Events

#$events= Get-WinEvent -computername $ComputerName -FilterHashtable @{ logname = "Key Management Service"; ID = "12290"; StartTime = [datetime]::today}

# Yesterday's Last 5 Events (-Newest 5)

#$events= Get-WinEvent -computername $ComputerName -Newest 5 -FilterHashtable @{ logname = "Key Management Service"; ID = "12290"; StartTime = (Get-Date).AddDays(-1); EndTime = [datetime]::today}

 

 

```
