## PS Remoting
- Enables a computer to receive remote Powershell commands
- Enabled by default on Windows Server

## WinRM
- Microsoft's Implementation of Web Services Management (WS-Man) which allows execution of management commands over a network. 
- WS-Man stands for Web Services Management is a protocol for management of devices over a network. 
- PowerShell remoting uses WinRM for communication

## SAM 
- Security Account Manager
- Stored on a local computer and contains information about local accounts and groups
- `C:\Windows\System32\config\SAM`
- AD Accounts are stored in the domain controller in `NTDS.dit`

## Security Principals
- Identities that Windows can assign permissions to
- An entity with SID
- They can be Users, Groups, Computer Accounts
- Local Principal is stored in SAM, Domain Principal is stored in the AD



