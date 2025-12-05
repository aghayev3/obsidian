
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
- `$dc = New-PSSession -ComputerName <ip or name> -Credential (Get-Credential)` to save the results into `$dc` variable
- `echo $dc`
- `Copy-Item <filename> -ToSession $dc <file location on the remote>`
- `Enter-PSSession $dc` 
- 

## WinRM
- `get-item wsman:\localhost\Client\TrustedHosts` to get the current Trusted Hosts
- `set-item wsman:\localhost\Client\TrustedHosts -value <value>` to set the value to something
## Starting a Service
- `Start-Service <servicename>` 
- For example `Start-Service WinRM` which is necessary to add a remote device to WinRM Trusted hosts

## Hostname
- `hostname` lol

## Generating SSH Keys (for GitHub)
- `SSH-Keygen` 
- Add the public key to GitHub
- 
## Installing Active Directory 
- `ipconfig \all` to verify the interface details
- `sconfig` and select the network settings to see the adapter index
- Set a static IP address for the Domain Controller
- Also set the DNS to be the same as the IP of the DC
- `Get-WindowsFeature | ? {$_.NAME -LIKE "AD*"}` to see a list of Windows Features starting with "AD"
- `Install-WindowsFeature AD-Domain-Services -IncludeManagementTools`
- `Import-Module ADDSDeployment`
- `Install-ADDSForest`
- After restarting, make sure you set the DNS again
- Make sure to change the joining client's DNS address to be the DC
- `Add-Computer -DomainName <domainname> -Credential Domain\Administrator -Force -Restart` to join the computer to the AD

## Change the DNS address
- `Get-NetIPAddress -IPAddress <ip>` which gives you the interface index
- `Set-DNSClientServerAddress -InterfaceIndex <iface index> -ServerAddresses <IPs>`

