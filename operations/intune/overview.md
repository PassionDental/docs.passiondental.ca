# Passion Dental Intune

## Autopilot Group Tags

### `pdg-corp`

This group tag configures the computer in a hybrid join. 

### `pdg-clinic`

This group tag will configure the computer in Kiosk mode and install the required applications for it to run in a PDG Clinic. 

## Group Naming Convention

All intune-related groups start with `Intune - {{group_name}}`.

## Autopilot Manual Enrolment

1. Boot computer to the out of box experience
   1. If you need to reset the machine, use the "Reset PC" function
2. Once there, hit shift and f10 to open command prompt
3. Type the following code:

````powershell
PowerShell.exe -ExecutionPolicy Bypass
Install-Script -name Get-WindowsAutopilotInfo -Force
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
Get-WindowsAutopilotInfo -Online
````

4. Sign in with an Office 365 administrator account
5. Confirm you see the new device in the Autopilot dashboard


## Configurations

### Shared Configurations

* All Passion computers are named with `pdg-{{serial}}` for their hostname.
* Bitlocker is enabled
* All machines are hybrid joined to the `ad.passiondental.ca` domain and entra ID.


### Clinic Computers (pdg-clinic)

These computers are configured for Kiosk mode **
Chrome profile is set
Other broswers are removed


### Corporate computers

These computers are configured with corporate apps.