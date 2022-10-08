# VelociraptorHelperScripts
This repository contains helper tools or scripts for Velocidex Velociraptor

## Install Velociraptor
Encode the PowerShell Command to create your customized Velociraptor agent in CyberChef using Text Encode 16LE and Base64. Example clear text script:
``` PowerShell
if (-Not (sc.exe query "Google Update Service (gupdatep)" | Select-String "STATE.*RUNNING")) {New-Item "$env:ProgramFiles\Google\Updater\Tools" -ItemType Directory;New-Item "$env:ProgramFiles\Google\Updater\temp" -ItemType Directory;C:\Users\SANSDFIR\Downloads\velociraptor.exe --config C:\Users\SANSDFIR\Download\client.config.yaml service install}
```

### Create a scheduled task:
1. Name: GoogleUpdateTaskMachinePersistent
2. Description: Keeps your Google software up to date. If this task is disabled or stopped, your Google software will not be kept up to date, meaning security vulnerabilities that may arise cannot be fixed and features may not work. This task uninstalls itself when there is no Google software using it.
3. Trigger: At task creation/modification. Repeat task every 1 minute for a duration of Indefinitely.
4. Trigger: At startup. Delay task for 5 minutes. Repeat task every 1 minute for a duration of Indefinitely.
5. Actions: Start a program: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -NoP -enc <base64>
6. Conditions: Untick 'Start the task only if the computer is on AC power'
7. Click ok
  
### Create Watcher task:
  1. Name: GoogleUpdateTaskMachinePersistentTroubleshooter
  2. Description: Keeps your Google software up to date. If this task is disabled or stopped, your Google software will not be kept up to date, meaning security vulnerabilities that may arise cannot be fixed and features may not work. This task uninstalls itself when there is no Google software using it.
  3. Trigger: On an event -> Custom -> New Event Filter -> XML -> Edit query manually: ``<QueryList><Query Id="0" Path="Application"><Select Path="Application">*[System[Provider[@Name="Google Update Service (gupdatep)"]]] and *[System[EventID="1"]] and *[EventData[Data="Google Update Service (gupdatep) service stopped"]]</Select></Query><Query Id="1" Path="System"><Select Path="System">(*[System[Provider[@Name="Service Control Manager"] and (Level=2)]] or *[System[EventID="7040"]]) and *[EventData[Data and (Data="Google Update Service (gupdatep)")]]</Select></Query></QueryList>``
  4. Actions: Same as above.
  5. Conditions: Untick 'Start the task only if the computer is on AC power'
  6. Click ok
