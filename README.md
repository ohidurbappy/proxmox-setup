# proxmox-setup
Basic Proxmox setup instructions

### Increase the storage

1. Delete `local-lvm` volume from storage section. Use 'Folder View' on the left.

2. Open shell and type the following commands:
  
 ```bash
 lvremove /dev/pve/data
 lvresize -l 100%FREE /dev/pve/root
 resize2fs /dev/mapper/pve-root

 ```
 
 3. Edit the storage section to use `local` for containers and virtual machines.
 
 
 ### For laptops to close the lid
 
 Edit the file: /etc/systemd/logind.conf
 
 ```
 nano /etc/systemd/logind.conf
 
 ```
 
 Add the following two lines:
 
 ```
 HandleLidSwitch=ignore
 HandleLidSwitchDocked=ignore
 ```
 
 Restart the service
 
 ```
 systemctl restart systemd-logind.service
 ```
 
 ### Turn off the screen after some period of time
 
 ```
 nano /etc/default/grub
 ```
 
Change the line:
 
```
GRUB_CMDLINE_LINUX="consoleblank=300"
```

To update the grub

```
update-grub
```


To solve auto log out from the web ui

```
touch /etc/pve/authkey.pub*
```

Disable no subscription alert

```
curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/rickycodes/pve-no-subscription/main/no-subscription-warning.sh | sh
```

 
 Networkchuck video: https://www.youtube.com/watch?v=_u8qTN3cCnQ
