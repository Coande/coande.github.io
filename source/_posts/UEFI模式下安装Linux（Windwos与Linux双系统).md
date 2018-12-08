title: UEFI模式下安装Linux（Windwos与Linux双系统)
date: 2015-11-02 15:44:12
tags:
	- 双系统
	- Linux
categories:
	- 技巧
---
我的系统原本是Windows10的，UEFI+GPT，今天我又装了个Kali Linux 2.0，即Windows10+Kali2.0双系统，在这里记录一下。<!--more-->

MBR下安装双系统很容易，先安装window再安装Linux就可以轻松搞定了；UEFI下安装就稍稍麻烦点，但也不难。UEFI启动的其它版本Windws系统的基础上安装其它Linux发行版估计也差不多，我这里按我的情况来写下。

昨天百度看了很多资料，还是一头雾水，一些人说这样，一些人说那样，弄的有点晕。后来Google一下，就看了前面几条搜索结果，就找到了视频教程，很清晰明了，按照视频的步骤去做就可以了，所以不得不说百度不了就Google一下吧~直接上视频（Youtube喔，你懂的）：
<iframe width="560" height="315" src="https://www.youtube.com/embed/7m6ALEZKO3Q" frameborder="0" allowfullscreen></iframe>

**我概括一下：**

准备条件：网络。

* 首先，做好Linux的启动盘。缩小其它分区留个未使用的分区给kali。
* Legacy或者CMS模式下安装Linux。要注意的是，安装过程中提示设置软件源，no掉（我不知道为什么，视频就是这样，知道的告诉我吧），后续再设置；GRUB不要安装。待会手动安装efi的GRUB。
* 安装好后重启，BIOS中设置好使用UEFI模式。进入启动盘的Live模式。（视频中叫使用其它可以在UEFI中启动并带Live功能的启动盘，其实前面做好的Linux启动盘就完全可以了。下一步之前，如果你后悔了，可以什么都不干，还可以直接进入你的Windows系统~~\~）
* 然后嘛，跟着敲吧，再说一次，需要有网络~下面贴上我的可以参考下：
*先说明一下，用live进去后作为live的U盘识别为我的第一硬盘，即sda，我的真实硬盘是第二个硬盘，所以是sdb，sdb1也就是efi分区，我的kali安装在sdb8中。至于什么是sda什么是sdb都不知道的就劝你别搞了~~\~*

```
root@kali:~# [ -d /sys/firmware/efi ] && echo UEFI || echo BIOS
UEFI
root@kali:~# gdisk -l /dev/sda
GPT fdisk (gdisk) version 0.8.10

Partition table scan:
  MBR: MBR only
  BSD: not present
  APM: not present
  GPT: not present


***************************************************************
Found invalid GPT and valid MBR; converting MBR to GPT format
in memory. 
***************************************************************

Disk /dev/sda: 8168448 sectors, 3.9 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): B86C2984-459F-4A1B-991E-A559F54FF9F3
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 8168414
Partitions will be aligned on 64-sector boundaries
Total free space is 1683069 sectors (821.8 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1              64         6324223   3.0 GiB     0700  Microsoft basic data
   2         6324224         6485375   78.7 MiB    0700  Microsoft basic data
root@kali:~# gdisk -l /dev/sdb
GPT fdisk (gdisk) version 0.8.10

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.
Disk /dev/sdb: 976773168 sectors, 465.8 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): E6EFCAC1-7174-4FC9-ADB0-F1624669A899
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 976773134
Partitions will be aligned on 16-sector boundaries
Total free space is 1845230 sectors (901.0 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048          206847   100.0 MiB   EF00  EFI system partition
   2         2050048         2312191   128.0 MiB   0C01  Microsoft reserved ...
   3         2312192       212027391   100.0 GiB   0700  Basic data partition
   4       347631632       557344783   100.0 GiB   0700  Basic data partition
   5       557344784       767059983   100.0 GiB   0700  Basic data partition
   6       767059984       976773134   100.0 GiB   0700  Basic data partition
   7       212027392       215932927   1.9 GiB     8200  
   8       215932928       347631615   62.8 GiB    8300  
root@kali:~# mount /dev/sdb8 /mnt
root@kali:~# for i in /dev /dev/pts /proc /sys ; do mount -B $i /mnt/$i ; done
root@kali:~# gdisk -l /dev/sdb
GPT fdisk (gdisk) version 0.8.10

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.
Disk /dev/sdb: 976773168 sectors, 465.8 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): E6EFCAC1-7174-4FC9-ADB0-F1624669A899
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 976773134
Partitions will be aligned on 16-sector boundaries
Total free space is 1845230 sectors (901.0 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048          206847   100.0 MiB   EF00  EFI system partition
   2         2050048         2312191   128.0 MiB   0C01  Microsoft reserved ...
   3         2312192       212027391   100.0 GiB   0700  Basic data partition
   4       347631632       557344783   100.0 GiB   0700  Basic data partition
   5       557344784       767059983   100.0 GiB   0700  Basic data partition
   6       767059984       976773134   100.0 GiB   0700  Basic data partition
   7       212027392       215932927   1.9 GiB     8200  
   8       215932928       347631615   62.8 GiB    8300  
root@kali:~# mkdir -p /mnt/boot/efi
root@kali:~# mount /dev/sdb1 /mnt/boot/efi
root@kali:~# chroot /mnt "/bin/bash"
root@kali:/# apt-get remove grub-*
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Note, selecting 'grub-doc' for regex 'grub-*'
Note, selecting 'grub-coreboot' for regex 'grub-*'
Note, selecting 'grub-efi-ia32' for regex 'grub-*'
Note, selecting 'grub-efi-amd64' for regex 'grub-*'
Note, selecting 'grub-efi-ia64' for regex 'grub-*'
Note, selecting 'grub-common' for regex 'grub-*'
Note, selecting 'grub-ieee1275' for regex 'grub-*'
Note, selecting 'grub2-common' for regex 'grub-*'
Note, selecting 'grub-linuxbios' for regex 'grub-*'
Note, selecting 'grub' for regex 'grub-*'
Note, selecting 'grub-legacy' for regex 'grub-*'
Note, selecting 'grub2' for regex 'grub-*'
Note, selecting 'grub-pc-bin' for regex 'grub-*'
Note, selecting 'grub-yeeloong' for regex 'grub-*'
Note, selecting 'grub-efi' for regex 'grub-*'
Note, selecting 'grub-pc' for regex 'grub-*'
Note, selecting 'grub-xen-host' for regex 'grub-*'
Note, selecting 'grub-emu' for regex 'grub-*'
Note, selecting 'grub-xen' for regex 'grub-*'
Note, selecting 'grub-legacy-doc' for regex 'grub-*'
Package 'grub-xen-host' is not installed, so not removed
Package 'grub2' is not installed, so not removed
Package 'grub' is not installed, so not removed
Package 'grub-coreboot' is not installed, so not removed
Package 'grub-efi-amd64' is not installed, so not removed
Package 'grub-efi-ia32' is not installed, so not removed
Package 'grub-ieee1275' is not installed, so not removed
Package 'grub-legacy' is not installed, so not removed
Package 'grub-xen' is not installed, so not removed
Package 'grub-doc' is not installed, so not removed
Package 'grub-legacy-doc' is not installed, so not removed
Package 'grub-efi' is not installed, so not removed
Package 'grub-efi-ia64' is not installed, so not removed
Package 'grub-linuxbios' is not installed, so not removed
Package 'grub-yeeloong' is not installed, so not removed
Package 'grub-emu' is not installed, so not removed
The following packages will be REMOVED:
  grub-common grub-pc grub-pc-bin grub2-common
0 upgraded, 0 newly installed, 4 to remove and 59 not upgraded.
After this operation, 19.4 MB disk space will be freed.
Do you want to continue? [Y/n] Y
(Reading database ... 323261 files and directories currently installed.)
Removing grub-pc (2.02~beta2-22) ...
Removing grub2-common (2.02~beta2-22) ...
Removing grub-pc-bin (2.02~beta2-22) ...
Removing grub-common (2.02~beta2-22) ...
Processing triggers for man-db (2.7.0.2-5) ...
Processing triggers for install-info (5.2.0.dfsg.1-6) ...
root@kali:/# echo "deb http://http.kali.org/kali sana main non-free contrib" >> /etc/apt/sources.list
root@kali:/# apt-get update
Get:1 http://http.kali.org sana InRelease [20.3 kB]                           
Get:2 http://http.kali.org sana/main amd64 Packages [12.8 MB]
Ign http://http.kali.org sana/contrib Translation-en_US                                                                                              
Ign http://http.kali.org sana/contrib Translation-en                                                                                                 
Ign http://http.kali.org sana/main Translation-en_US                                                                                                 
Ign http://http.kali.org sana/main Translation-en                                                                                                    
Ign http://http.kali.org sana/non-free Translation-en_US                                                                                             
Ign http://http.kali.org sana/non-free Translation-en                                                                                                
Get:3 http://http.kali.org sana/non-free amd64 Packages [164 kB]                                                                                     
Get:4 http://http.kali.org sana/contrib amd64 Packages [87.7 kB]                                                                                     
Hit http://security.kali.org sana/updates InRelease                                                                                                  
Get:5 http://security.kali.org sana/updates/main Sources [74.5 kB]
Get:6 http://security.kali.org sana/updates/contrib Sources [20 B]
Get:7 http://security.kali.org sana/updates/non-free Sources [20 B]                                                                                  
Ign http://security.kali.org sana/updates/contrib Translation-en_US                                                                                  
Ign http://security.kali.org sana/updates/contrib Translation-en                                                                                     
Ign http://security.kali.org sana/updates/main Translation-en_US                                                                                     
Ign http://security.kali.org sana/updates/main Translation-en                                                                                        
Ign http://security.kali.org sana/updates/non-free Translation-en_US                                                                                 
Ign http://security.kali.org sana/updates/non-free Translation-en                                                                                    
Hit http://security.kali.org sana/updates/main amd64 Packages                                                                                        
Hit http://security.kali.org sana/updates/contrib amd64 Packages                                                                                     
Hit http://security.kali.org sana/updates/non-free amd64 Packages                                                                                    
Fetched 13.1 MB in 2min 31s (86.8 kB/s)                                                                                                              
Reading package lists... Done
root@kali:/# apt-get install -y grub-efi
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following extra packages will be installed:
  efibootmgr grub-common grub-efi-amd64 grub-efi-amd64-bin grub2-common libefivar0
Suggested packages:
  multiboot-doc grub-emu xorriso
The following NEW packages will be installed:
  efibootmgr grub-common grub-efi grub-efi-amd64 grub-efi-amd64-bin grub2-common libefivar0
0 upgraded, 7 newly installed, 0 to remove and 97 not upgraded.
Need to get 4,015 kB of archives.
After this operation, 19.2 MB of additional disk space will be used.
Get:1 http://http.kali.org/kali/ sana/main libefivar0 amd64 0.15-3 [14.8 kB]
Get:2 http://http.kali.org/kali/ sana/main efibootmgr amd64 0.11.0-3 [43.3 kB]
Get:3 http://http.kali.org/kali/ sana/main grub-common amd64 2.02~beta2-22 [2,725 kB]                                                                
Get:4 http://http.kali.org/kali/ sana/main grub2-common amd64 2.02~beta2-22 [504 kB]                                                                 
Get:5 http://http.kali.org/kali/ sana/main grub-efi-amd64-bin amd64 2.02~beta2-22 [652 kB]                                                           
Get:6 http://http.kali.org/kali/ sana/main grub-efi-amd64 amd64 2.02~beta2-22 [73.0 kB]                                                              
Get:7 http://http.kali.org/kali/ sana/main grub-efi amd64 2.02~beta2-22 [2,582 B]                                                                    
Fetched 4,015 kB in 3min 33s (18.8 kB/s)                                                                                                             
Preconfiguring packages ...
Selecting previously unselected package libefivar0:amd64.
(Reading database ... 322826 files and directories currently installed.)
Preparing to unpack .../libefivar0_0.15-3_amd64.deb ...
Unpacking libefivar0:amd64 (0.15-3) ...
Selecting previously unselected package efibootmgr.
Preparing to unpack .../efibootmgr_0.11.0-3_amd64.deb ...
Unpacking efibootmgr (0.11.0-3) ...
Selecting previously unselected package grub-common.
Preparing to unpack .../grub-common_2.02~beta2-22_amd64.deb ...
Unpacking grub-common (2.02~beta2-22) ...
Selecting previously unselected package grub2-common.
Preparing to unpack .../grub2-common_2.02~beta2-22_amd64.deb ...
Unpacking grub2-common (2.02~beta2-22) ...
Selecting previously unselected package grub-efi-amd64-bin.
Preparing to unpack .../grub-efi-amd64-bin_2.02~beta2-22_amd64.deb ...
Unpacking grub-efi-amd64-bin (2.02~beta2-22) ...
Selecting previously unselected package grub-efi-amd64.
Preparing to unpack .../grub-efi-amd64_2.02~beta2-22_amd64.deb ...
Unpacking grub-efi-amd64 (2.02~beta2-22) ...
Selecting previously unselected package grub-efi.
Preparing to unpack .../grub-efi_2.02~beta2-22_amd64.deb ...
Unpacking grub-efi (2.02~beta2-22) ...
Processing triggers for man-db (2.7.0.2-5) ...
Processing triggers for install-info (5.2.0.dfsg.1-6) ...
Setting up libefivar0:amd64 (0.15-3) ...
Setting up efibootmgr (0.11.0-3) ...
Setting up grub-common (2.02~beta2-22) ...
Setting up grub2-common (2.02~beta2-22) ...
Setting up grub-efi-amd64-bin (2.02~beta2-22) ...
Setting up grub-efi-amd64 (2.02~beta2-22) ...
Setting up grub-efi (2.02~beta2-22) ...
Processing triggers for libc-bin (2.19-18) ...
root@kali:/# grub-mkconfig -o /boot/grub/grub.cfg
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-4.0.0-kali1-amd64
Found initrd image: /boot/initrd.img-4.0.0-kali1-amd64
  No volume groups found
Adding boot menu entry for EFI firmware configuration
done
root@kali:/# grub-install /dev/sdb
Installing for x86_64-efi platform.
Installation finished. No error reported.
root@kali:/# exit
exit
root@kali:~# umount /mnt/boot/efi/
root@kali:~# umount /mnt/dev/pts
root@kali:~# umount /mnt/dev
root@kali:~# umount /mnt/proc
root@kali:~# umount /mnt/sys
root@kali:~# umount /mnt/
root@kali:~# umount /mnt/
root@kali:~# reboot
```

* 重启后可以直接进入Kali了，但是grub菜单中还没有Windows的启动项。还需要敲敲：
```
root@kali:~# grub-mkconfig -o /boot/grub/grub.cfg
Generating grub configuration file ...
Found background image: /usr/share/images/desktop-base/desktop-grub.png
Found linux image: /boot/vmlinuz-4.0.0-kali1-amd64
Found initrd image: /boot/initrd.img-4.0.0-kali1-amd64
  No volume groups found
Found Windows Boot Manager on /dev/sda1@/efi/Microsoft/Boot/bootmgfw.efi
Adding boot menu entry for EFI firmware configuration
done
```
* reboot看看有没有windows的启动项吧。然后想干嘛干嘛~~~

