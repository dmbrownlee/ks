
# Overview

The kickstart files in this directory install Ansible and setup a cronjob that runs ```ansible-pull``` to automatically check for updates to the Ansible files an run the local.yml playbook when changes are detected.

## Rocky
Boot from the installation media, use the cursor keys to highlight the menu option to install Rocky, and press 'e' __instead of pressing return__ so you can edit the menu option (the keys to press are displayed at the bottom of the screen in case you forget).  Use the cursor keys to go down to the line beginning with "linux" and use Ctrl-e to jump to the end of that line.  Once there, add the following to the end of the line:
```
inst.ks=https://raw.githubusercontent.com/dmbrownlee/ks/release/kickstart/rocky/ks.cfg
```

Additionally, you can pass a few optional arguments beginnin with ```kspost.``` that will be used in the ```%post``` section:
```
kspost.fqdn:
  The fully qualified name of the host you are installing.  If set, the
  hostname will be updated to this before ansible runs (so ansible will use
  this instead of localhost).
kspost.luks_password:
  Replaces the default LUKS password. You may not want to use this as it 
  leaves the disk encryption password in the clear on the disk in the install
  log.  On the other hand, the disk is encrypted so...
kspost.ansible_vault_password_file:
  URL to the ansible vault password file.  It is assumed this URL is only
  accessible from the provisioning network.
kspost.ansible_branch:
  The git branch ansible-pull will use.  Defaults to "release" if not
  specified.
```
Then press Ctrl-x (as displayed at the bottom of the screen) to begin the installation.

The ks.cfg kickstart file is mostly automated but you will have to follow the text screen prompts to select the disk you want to install on.  If you are already familiar with how Linux names disks and know your system disk is sda, vda, or mmc, you can use the corresponding kickstart file instead of the non-specific ks.cfg file to skip the disk sellection and have a fully automated install
