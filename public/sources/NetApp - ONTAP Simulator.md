```
tags: NetApp #ONTAP #workingdocument #net
```
# My Environment

- MacBook Pro 2018
	- 2.9 Ghz
	- 32GB Memory
	- Ventura 13.2.1
- VirtualBox 7.0.7
- ONTAP Simulator 9.11.1


# Downloads 
- https://kb.netapp.com/Advice_and_Troubleshooting/Data_Storage_Software/ONTAP_OS/Where_can_the_NetApp_ONTAP_9_Simulator_be_downloaded
- https://madlabber.wordpress.com/2020/03/14/converting-the-ontap-simulator-to-work-in-virtualbox/
	- https://github.com/madlabber/vsim2vbox

# Script
```bash
#!/bin/bash
#name="vsim-netapp-DOT9.7-cm_nodar"
#name="vsim-netapp-DOT9.9.1-cm_nodar"
name="vsim-netapp-DOT9.11.1-cm_nodar"
memory=6192
IDE00="vsim-NetAppDOT-simulate-disk1.vmdk"
IDE01="vsim-NetAppDOT-simulate-disk2.vmdk"
IDE10="vsim-NetAppDOT-simulate-disk3.vmdk"
IDE11="vsim-NetAppDOT-simulate-disk4.vmdk"

#need to make sure virtualbox is installed
if [ -z "$(which vboxmanage)" ];then echo "vboxmanage not found";exit;fi

# Extract the OVA archive
tar -xzvf "$name".ova

#Make a new VM from scratch
vboxmanage createvm --name "$name" --ostype "FreeBSD_64" --register
vboxmanage modifyvm "$name" --ioapic on
vboxmanage modifyvm "$name" --vram 20
vboxmanage modifyvm "$name" --cpus 2
vboxmanage modifyvm "$name" --memory "$memory"

# Add Network Adapters
vboxmanage modifyvm "$name" --nic1 intnet --nictype1 82545EM --cableconnected1 on
vboxmanage modifyvm "$name" --nic2 intnet --nictype2 82545EM --cableconnected2 on
vboxmanage modifyvm "$name" --nic3 intnet --nictype3 82545EM --cableconnected3 on
vboxmanage modifyvm "$name" --nic4 intnet --nictype4 82545EM --cableconnected4 on

# Add serial ports
vboxmanage modifyvm "$name" --uart1 0x3F8 4
vboxmanage modifyvm "$name" --uart2 0x2F8 3

# Add a blank floppy
vboxmanage storagectl "$name" --name floppy --add floppy --controller I82078 --portcount 1
vboxmanage storageattach "$name" --storagectl floppy --device 0 --medium emptydrive

# Add an IDE controller
vboxmanage storagectl "$name" --name IDE    --add ide    --controller PIIX4  --portcount 2

# Attach VMDKs
vboxmanage storageattach "$name" --storagectl IDE --port 0 --device 0 --type hdd --medium "$IDE00"
vboxmanage storageattach "$name" --storagectl IDE --port 0 --device 1 --type hdd --medium "$IDE01"
vboxmanage storageattach "$name" --storagectl IDE --port 1 --device 0 --type hdd --medium "$IDE10"
vboxmanage storageattach "$name" --storagectl IDE --port 1 --device 1 --type hdd --medium "$IDE11"

# Jon's Changes
vboxmanage modifyvm "$name" --pae=on

# Export the finished VM to a new OVA file
vboxmanage export "$name" -o "$name"-vbox.ova

# cleanup
vboxmanage unregistervm "$name" --delete

```

# Setup for Node 1

Login to the system as admin ( no password )


```bash
cluster setup
```

![[Pasted image 20230320091533.png]]

![[Pasted image 20230320091858.png]]


![[Pasted image 20230320092206.png]]

- We don't set license keys at this point just press return over that prompt
- Note we need to change the network interface from e0d to e0c
![[Pasted image 20230320092335.png]]

![[Pasted image 20230320092746.png]]

![[Pasted image 20230320092904.png|1000]]



# Setup for Node 2

- Boot the second image and press space at the Hit enternto boot imeddaitely prompt as we need to change the serial number

![[Pasted image 20230320115509.png]]

Run cluster setup for the second node

![[Pasted image 20230320115813.png]]


