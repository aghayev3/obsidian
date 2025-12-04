
## Disable SConfig at sign-in
- `Set-SConfig -AutoLaunch $false`

## Reboot
- `shutdown /r /t 0`

## Shutdown 
- `shutdown /s /t 0`

## PS-Remoting
- `Enable-PSRemoting` configures the computer to receive commands
- `New-PSSession -ComputerName <ip or name> -Credential (Get-Credential)` to initiate a new session 
- `Enter-PSSession <id>` to enter the session. You get the ID of the session after the `New-Session` command 

## WinRM
- `get-item wsman:\localhost\Client\TrustedHosts` to get the current Trusted Hosts
- `set-item wsman:\localhost\Client\TrustedHosts -value <value>` to set the value to something
## Starting a Service
- `Start-Service <servicename>` 
- For example `Start-Service WinRM` which is necessary to add a remote device to WinRM Trusted hosts

