I'm working on application which run PowerShell scripts related to Microsoft Office 365 service.
Application is built with 32bit arhitecture.
Development Operating System is Windows 10 64bit.

Based on application arhitecture Microsoft Visual Studio run 32bit PowerShell.

Problem is that MSOnline module (Office 365 PowerShell Module) cant be run in PowerShell 32bit on Windows 64bit. It can be run in PowerShell 64bit.

My solution (all files are in this repository):

- Install "Microsoft Online Services Sign-In Assistant for IT Professionals RTW 64bit" (msoidcli_64.msi)
- Install "Windows Azure Active Directory Module for Windows PowerShell" (AdministrationConfig-EN.msi) This is version 1.0.0 (newer version doesn't work)
- Copy "MSOnline" folder from "Modules" to:
	- C:\Windows\System32\WindowsPowerShell\v1.0\Modules
	- C:\Windows\SysWOW64\WindowsPowerShell\v1.0\Modules
- Restart Microsoft Visual Studio

Now you should be able to run MSOnline module in PowerShell 32bit

Simple test case (run in PowerShell 32bit):

```powershell
$UserCredential = Get-Credential

Connect-MsolService -Credential $UserCredential
```


