## Manjaro VBox guest setup

### 2019-05-08

#### Install Guest Additions

```
xclip -sel clip < ~/.ssh/id_rsa.pub
```

#### Setup Shared Folders

**On the host** add the folder to the VB configuration for the machine:

- chose the host directory to share
- enter a name which will be the mount name on the guest
- do **not** enable auto-mount, but enable _Make Permanent_
- leave the mount point blank

**Then start the guest** and:

- in the home directory create the folders to be mounted. Their names do not need to match the mount names from above
- `sudo vi /etc/fstab` to add the mounts:  
  `mount-name /home/ronald/folder vboxsf uid=1000,gid=1000 0 0`  
  where _folder_ is the name of the folder to be mounted from above
- reboot the guest

#### Setup Window Resolution - Frame Size

```
xclip -sel clip < ~/.ssh/id_rsa.pub
```

#### documentation

- [Installing Guest Additons (Arch Wiki)](https://wiki.archlinux.org/index.php/VirtualBox#Installation_steps_for_Arch_Linux_guests)
- [Setting Up VirtualBox Shared Folders (Josh Braun’s Blog)](http://wideaperture.net/blog/?p=4034)
