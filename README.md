# FoundryVTT Install with Caddy and PM2

This script assumes you are using Debian 10, Ubuntu 20.04 LTS, Ubuntu 22.04 LTS or Debian 11. It is a forked/modified version of maserspark's stackscript on Linode. You can use this to install and setup Foundry on a fresh system, or you can create additional Foundry instances with it. Once done, you'll have a Foundry instance managed with PM2 and available to the interwebs with SSL via Caddy.

This runs as root and will either create a system user for you or assume that you already have one as specified by the coresponding variable. In order to manage Foundry via PM2, commands will need to be ran as sudo.

**Make sure you are complying with the FoundryVTT Software License before installing additional instances**

> You may install and activate the software on one or more computers, but only one hosted instance of the software may be accessible to users other than the license owner at any given time. Hosting multiple accessible instances of the software is permitted by owning a corresponding number of software licenses.

https://foundryvtt.com/article/license/

## Variables

### FOUNDRY_URL

This is the download URL for Foundry which can be obtained via the Purchased Software Licenses page for your FoundryVTT account. Ensure you have "Linux/NodeJS" selected as the operating system before clicking **Timed URL**.

### FOUNDRY_HOSTNAME

default=""

If you have a domain for Foundry, input that here. An example would be "foundry.example.com".

### FOUNDRY_APP_DIR

default="/opt/foundryvtt"

If you have no reason to change this, that means you probably shouldn't.

### FOUNDRY_DATA_DIR

default="/opt/foundrydata"

If you have no reason to change this, that means you probably shouldn't.

### FOUNDRY_PORT

default="30000"

If this is your first installation, leave this as default (unless something else is using that port). If you are adding an additional instance, change this to an open port (most people can probably get away with incrementing it by 1).

### FOUNDRY_PM2_NAME

default="foundry"

If this is your first installation, you can change it if you like; but it doesn't matter too much.

### FOUNDRY_USER

default="foundry"

This is the system user that will have ownership over Foundry's files. If you are installing Foundry for the first time and want to use an existing user, comment out the following line:
```
useradd -r $FOUNDRY_USER
```

## Installing Foundry for the First Time

If you run the script without editing, the following will occur:

* The URL and HOSTNAME will be blank, making your instance accessible locally only unless otherwise changed
* Foundry's App and Data directories will be installed to /opt/foundryvtt and /opt/foundrydata respectively
* The local port number will be 30000
* PM2 will be installed and will use "foundry" as the name to manage it
* A system user named "foundry" will be created and given ownership over the Foundry directories

## Installing Additional Foundry Instances

For additional instances, change the variables to whatever you desire (except the FOUNDRY_USER presumably), and run the script.

## Managing with PM2

PM2 is a process manager that aides in controlling your Foundry app. If Foundry crashes or shuts down involuntary, PM2 will automatically restart it.

List all PM2 processes
```
sudo pm2 list
```

Start/Stop Foundry
```
sudo pm2 start FOUNDRY_PM2_NAME
```
```
sudo pm2 stop FOUNDRY_PM2_NAME
```

Restart Foundry
```
sudo pm2 restart FOUNDRY_PM2_NAME
```
---
Fool of a Took!
