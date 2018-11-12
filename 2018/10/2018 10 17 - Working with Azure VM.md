# Working with Azure VM

## Control VM using Azure CLI

You can use Azure-cli to start up and stop an Azure VM

```
az vm start -g resourceGroupName -n vmName
az vm stop -g resourceGroupName -n vmName
```

After that, you can get the IP address of the machine
```
az vm get-ip-addresses -g resourceGroupName -n vmName
```
This will return a JSON object that includes the IP address

## Log in to VM using SSH

Use Bash of Windows 10 WLS (Windows Linux Subsystem) to login to remote VM using SSH.

## Copy files from Windows to WLS

Windows files are mounted on WLS at `/mnt/c`  
To access files on the Desktop, use `/mnt/c/Users/Amr/Desktop`  