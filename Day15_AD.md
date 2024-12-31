# Day 15[Active_Directory]: Be it ever so heinous, there's no place as like Domain Controller!

## Story :
Ahead of SOC-mas, the team decided to do a routine security check of one of their Active Directory domain controllers. Upon some quick auditing, the team noticed something was off. Could it be? The domain controller has been breached? With sweat on their brows, the SOC team smashed the glass and hit the panic alarm.

## Learning Objectives : 
- Learn about the structures of Active Directory.
- Learn about common Active Directory attacks.
- Investigate a breach against an Active Directory.

## Abbreviations and Applications :
- [AD]() : Active Directory. 
- [DN]() : Distinguished Name.
- [DC]() : Domain Controller.
- [OU]() : Organizational Unit, are containers within a domain that help group objects based on departments, locations or functions for easier management.
- [LDAP]() : Lightweight Domain Access Protocol, this protocol is used to query and modify the directory.
- [GC]() : Global Catalog, is a searchable database within AD that contains a subset of information from all objects in the directory. This allows users and services to locate objects in any domain in the forest, even if those objects reside in different domains.
- [Kerberos]() : The default authentication protocol used by AD provides secure authentication by using tickets rather than passwords.
- [TGT]() : In Kerberos, a Ticket Granting Ticket (TGT) serves as a user's proof of authentication and allows a user to request service tickets from the KDC, which can then be used to connect to services across the network.
- [GPO]() : Group Polcy Object, is a feature in Windows Server that allows administrators to control user and computer settings across the network.
 

## Process Key Steps and Points :
- **Common Event ID's** :
  |**Event ID**|**Description**|
  |----|----|
  |4624|A user account has logged on|
  |4625|	A user account failed to log on|
  |4672|	Special privileges (i.e. SeTcbPrivilege) have been assigned to a user|
  |4768|	A TGT (Kerberos) ticket was requested for a high-privileged account|
- 


## Commands Used :
- `Get-GPO -All`
- `Get-GPOReport -Name "SetWallpaper" -ReportType HTML -Path ".\SetWallpaper.html"`
- `Get-GPO -All | Where-Object { $_.ModificationTime } | Select-Object DisplayName, ModificationTime` 
- `Get-ADUser -Filter * -Properties MemberOf | Select-Object Name, SamAccountName, @{Name="Groups";Expression={$_.MemberOf}}`

## Questions, Hints and Answers :
1. On what day was Glitch_Malware last logged in?
   - Hint : Search in the Security Tab of Event Logs and use Find or Filter to get all logs of Glitch_Malware. `Look for Event : Logged On`
   - Ans : `07/11/2024`
2. What event ID shows the login of the Glitch_Malware user?
   - Hint : Same event as above and find the event ID
   - ![LogOnGlitch](/Screenshots/D15Q12.png)
   - Ans : `4624`
3. Read the PowerShell history of the Administrator account. What was the command that was used to enumerate Active Directory users?
   - Hint : Use `run` tool and check the file `%APPDATA%\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt`.
   - ![ADuser](/Screenshots/D15Q3.png)
   - Ans : `Get-ADUser -Filter * -Properties MemberOf | Select-Object Name`
4. Look in the PowerShell log file located in Application and Services Logs -> Windows PowerShell. What was Glitch_Malware's set password?
   - Hint : Go through the event logs and try finding set passwd by Glitch_Malware
   - ![GlitchPasswd](/Screenshots/D15Q4.png)
   - Ans : `SuperSecretP@ssw0rd!`
5. Review the Group Policy Objects present on the machine. What is the name of the installed GPO?
   - Hint : Use command `GET-GPO -all` in PowerShell.
   - ![GPO's](/Screenshots/D15Q5.png)
   - Ans : `Malicious GPO - Glitch_Malware Persistence`
