## demosmbc

This lab allow you to test NetApp SMBC base on the following lab:
------------------------------------------------------------------
- Lab: https://labondemand.netapp.com/lab/sl10628 

Script provide with this demo allow you to build a SnapMirror SMBC LAB
----------------------------------------------------------------------
Before to start this lab you have to configure each aggregagte on cluster1 and Cluster2 using System Manager 
- using Menu **STORAGE -> Tieres -> Add Local Tier**

Please run all the folowing on linux centos01 [ssh 192.168.0.61]
- Run the script **0-Setup-Linux-iscsi.sh** to install all required Linux Packages and confirm the gub update and reboot
- After reboot run **cat /proc/cmdline** to verify if *rdloaddriver=scsi_dh_alua* has been add in the running kernel
- Run the script **1-Install-Linux-NetAppTools.sh** to automatically to Install NetApp host utilities kit and the NetApp Mediator 1.2  
- Run the script **2-Setup-ontapsmbc.sh** to automatically build SMBC configuration the script will
- Run the script **3-Linux-LunDiscover.sh**
	- The script will disconver the LUN and create a LVM configuration on the LUN with and ext4 filessytem
	- Confirm the LUN will have 4-path on cluster1 and 4-path on clsuter2 [multipaht -ll]

# Example
Run the first script and confirm the grub update and 
````
[root@centos1 ~]# cd git/demosmbc/
[root@centos1 demosmbc]# ./0-Setup-Linux-iscsi.sh
...
...
Run: [grubby --args rdloaddriver=scsi_dh_alua --update-kernel /boot/vmlinuz-3.10.0-1160.6.1.el7.x86_64] [y/n]? : y
Reboot Linux now [y/n]? : y

[root@centos1 demosmbc]# ./0-Setup-Linux-iscsi.sh
...
...
Terminate
````
Run the second script to install NetApp Linux Package *Host utilities kit* and *NetApp Mediator 1.2* 
````
[root@centos1 demosmbc]# ./2-Setup-ontapsmbc.sh
...
...
...
Terminate
````
Check if the same Lun has been created on both cluster
````
[root@centos1 demosmbc]# ./runallcluster lun show
/usr/bin/sshpass
/usr/sbin/multipath
/usr/bin/rescan-scsi-bus.sh
Init SSH session host
=========================================================================================
cluster1 > lun show
Access restricted to authorized users

Last login time: 12/21/2020 19:44:32
Vserver   Path                            State   Mapped   Type        Size
--------- ------------------------------- ------- -------- -------- --------
SVM_SAN_P /vol/LUN01_P/LUN01              online  mapped   linux         9GB

=========================================================================================
cluster2 > lun show
Access restricted to authorized users

Last login time: 12/21/2020 19:44:32
Vserver   Path                            State   Mapped   Type        Size
--------- ------------------------------- ------- -------- -------- --------
SVM_SAN_S /vol/LUN01_S/LUN01              online  mapped   linux         9GB

````









NetApp SMBC Documentation is available here:
--------------------------------------------
- Doc: https://docs.netapp.com/us-en/ontap/smbc

