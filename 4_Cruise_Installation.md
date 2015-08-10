**This workshop will focus on installing Cruise server, local agent and remote agent.**

## Presentation ##

Cruise provides installers for different platforms such as Windows, Linux(Ubuntu/Redhat), Mac, Solaris. In this workshop we will take Windows installation for example. And we will require you to do pair working when installing remote agent.

## Prerequisite ##

  * Cruise server/agent Windows installers (in c:\workspace\ci\_tools\cruise\_installers).
  * Cruise license

## install cruise server ##
  1. Double click cruise-server-x.x.x-setup.exe and use the default settings to finish install
  1. Double "Cruise Server" on desktop to open cruise server web page
  1. Input the following license
```
USER: 

 CruiseTraining 

LICENSE KEY: 

giegDQfCZsqKzW1MZmEU0cdY/DXl1HzhGu/vlVV/7B2Z/0Eezklo6V+V6JVV
iHkbEoighgdUe0xwEOnKmKgZ/YZBMlwNjCahycNS5hQ11LymkiEmkYVXaviM
wjZaoAMy246AUD594XvXygO5tU1Jjlmv9DPkyuPe+UXL/MLaIlLwZpqeJdm7
cSwIvl6F3IyXoSQ/uYTj3JkxvOMFFrniHcmQOqfasj1C3LbRp7DWFjRYz1ip
YvYQZQsq2L0znLvlwqbY8KdXU48zJEfw9n1TnLAnbykopH1TLoD/z5MP0km/
PskbTqM0KKX07dD2ULN1RT6A93VUrLcHbihissr45w==
```
  1. Click "Save license", you'll got an message "Your license has been updated successfully"
  1. Click "Current Activity" tab on the top, Cruise will take you to the "Add New Pipeline" page
  1. Click "Agents" tab on the top, Cruise lists all the connected agents here, it's empty now
  1. Keep the browser open, and continue the following steps

## install cruise agent ##
  1. Double click cruise-agent-x.x.x-setup.exe and use the default settings to finish install
  1. Switch to the browser
  1. verify that one agent appears on the Agents tab

## install a remote agent (Pair working) ##
  * Get your IP address
    1. find someone to pair in this workshop
    1. open command line prompt
    1. type ipconfig to find your ip address
    1. tell your pair your ip address
  * Start cruise agent to connect to your pair
    1. type command: mkdir c:\workspace\agent
    1. type command: cd c:\workspace\agent
    1. type command: java -jar c:\workspace\ci\_tools\cruise\_installers\agent-bootstrapper.jar <IP address of your pair>
  * Check agents in Cruise server
    1. switch to the browser
    1. verify a new agent appears, and waiting for approval
    1. Approve the remote agent

# Presentation #

Demonstration about how Cruise Server works with agents.