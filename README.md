# demosmbc

This lab allow you to test NetApp SMBC base on the following lab:
------------------------------------------------------------------
- Lab: https://labondemand.netapp.com/lab/sl10628 

Script provide with this demo allow you to build a SnapMirror SMBC LAB
----------------------------------------------------------------------

Please run all the folowing on linux centos01 [ssh 192.168.0.61]
- Run the script [0-Setup-Linux-iscsi.sh] to install all required Linux Packages and confirm the gub update and reboot
- After reboot run [cat /proc/cmdline] to verify if [rdloaddriver=scsi_dh_alua] has been add in the running kernel
- Run the script [1-Install-Linux-NetAppTools.sh] to automatically to Install NetApp host utilities kit and the Mediator 1.2 require by SMBC 
- Setup the aggregagte on cluster1 and Cluster2 using System Manager (using Menu STORAGE -> Tieres -> Add Local Tier)
- Run the script [2-Setup-ontapsmbc.sh] to automatically build SMBC configuration the script will
	- Create Intercluster LIF on cluster1 and cluster2
	- Create cluster peer relation between cluster1 and cluster2
	- Create SVM Primary and SVM Secondary
	- Create Vserver peer relation
	- Install Mediator Certificate on cluster1 and clsuter2
	- Install Initialase a Mediator connection on cluster 1 and cluster2
	- Create Single Volume and a single LUN on cluster 1
	- Create a SnapMirror SMBC relation witih consitency group with this LUN
	- map the LUN to centos
- Run the script [3-Linux-LunDiscover.sh] 
	- The script will disconver the LUN and create a LVM configuration on the LUN with and ext4 filessytem
	- Confirm the LUN will have 4-path on cluster1 and 4-path on clsuter2 [multipaht -ll]


NetApp SMBC Documentation is available here:
--------------------------------------------
- Doc: https://docs.netapp.com/us-en/ontap/smbc

