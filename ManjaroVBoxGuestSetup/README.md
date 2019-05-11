## Manjaro VBox guest setup

### 2019-05-08

#### Install Manjaro Guest from ISO

- Download ISO from [Manjaro Downloads](), I chose the XFCE Edition
- Setup a virtual machine in VirtualBox:
  - add the ISO as Live CD
  - configure the monitor with 128 MB memory,  
    Graphics Controller **VBoxVga**, acceleration 3D, rest disabled
  - see _Shared Folders host part_ below
- Start the VM and run the installer, remove the Live CD and reboot
- upate all programs, reboot
- The VB Guest additions are installed by default (`virtualbox-guest-utils` and `KERNEL..-guest-modules`)

```
xclip -sel clip < ~/.ssh/id_rsa.pub
```

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
- `sudo gpasswd -a $USER vboxsf` to add user to group vboxsf
- `sudo vi /etc/fstab` to add the mounts:  
  `mount-name /home/ronald/folder vboxsf uid=1000,gid=1000,rw,dmode=700,fmode=600,x-systemd.automount 0 0`  
  where _folder_ is the name of the folder to be mounted from above
- reboot the guest
- instalar `rsyslog`

#### Setup Window Resolution - Frame Size

```
xclip -sel clip < ~/.ssh/id_rsa.pub
```

#### documentation

- [Installing Guest Additons (Arch Wiki)](https://wiki.archlinux.org/index.php/VirtualBox#Installation_steps_for_Arch_Linux_guests)
- [Setting Up VirtualBox Shared Folders (Josh Braun’s Blog)](http://wideaperture.net/blog/?p=4034)
- https://forum.manjaro.org/t/virtualbox-not-automounting-shared-folder-in-guest-manjaro-kde-v18-0-2/70886/5
- https://forum.manjaro.org/t/solved-virtualbox-shared-folder-is-empty-mount-failed/85792/3
- https://forum.manjaro.org/t/manjaro-guest-additions-problem/83603/8
