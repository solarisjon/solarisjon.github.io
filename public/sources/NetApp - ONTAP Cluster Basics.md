
#course #learning #udemy #ONTAP #NetApp #netapp_products 

---

```toc
```

---


```embed
title: 'Online Courses - Learn Anything, On Your Schedule | Udemy'
image: 'https://s.udemycdn.com/meta/default-meta-image-v2.png'
description: 'Udemy is an online learning and teaching marketplace with over 213,000 courses and 57 million students. Learn programming, marketing, data science and more.'
url: 'https://www.udemy.com/course/netapp-ontap-cluster-basics/learn/lecture/27845464#overview'
```

https://www.udemy.com/course/netapp-ontap-cluster-basics/learn/lecture/27845464#overview


---

# Concepts and Architecture

## Cluster Configurations

![[Pasted image 20230316091202.png|700]]
1 Node connected to one disk shelf - not HA , potential use as a backup server
HA Pair - 2 nodes connected to each other and all disks 
Multiple HA pairs to one cluster 24 nodes or 12 HA Pairs in a single cluster 
Cannot have odd number of nodes outsde of a 1 node
Custer interconnect - cluster config data to keeps nodes in sync , cluster heart beat, clusters private network , not accessed by clients, redundant network at least 2 per node
HA interconnect - used to mirror data from one controller to another , NVRAM mirroring, every node has NVRAM which stores data until written to drives


## Networking 

![[Pasted image 20230316092001.png|700]]
### Ports
Physical or virtual ports
Physical ports are network interface cards in the node
Virtual ports be 
	-interface groups which is a collection of physical ports for redundancy / bandwidth
	- VLAN ports configured on physical or virtual ports

### LIFs
Logical Interfaces
Multiple LIFS for one Port

### Cluster Interconnect Network
2 ports per node

### Management Network
managed via system manager, putty, ssh

### Data Network

## Physical and Logical Storage

### Physical
SSD or Spinning (HDD)
A group of disks  is in a Raid Group, one or more parity drives for protection from drive faulures
The raid groups are placed in an aggregate
aggregate managed by a single node in a HA pair
when you run out of space in an aggregate you can grow an aggregate but you cannot shrink it

![[Pasted image 20230318185058.png|700]]

### Logical Storage
part of the physical groups can be carved out in vols which can be accessed from clients these are called Flexible Volumes
volumes can be grown and shrunk manually or automatically
multiple flex vols can share an aggregate and can be moved to another aggregate in teh cluster

![[Pasted image 20230318185527.png|700]]

### Storage Virtual Machines ( SVM )
Live in a cluster and can be running or stopped
Used to be vservers '
Container for volumes or LIFSs
Volumes in a SVM need to be uniquely named
2 types of protocols NAS ( file level ) and SAN (block level )

![[Pasted image 20230318185849.png|700]]



## Data Protocols
NAS ( file level )
SAN ( block level )


# Interfacing with NetApp ONTAP

## System Manager 

- Graphical interface [[OnCommand System Manager]] , functionality changes often
- ClusterShell - CLI, intuitive
	- Admin Mode prompt is cluster1::>
		- set adv
		- set diag
	- Advanded and Diag mode 
	- Advanced 
		- set admin 
		- set diag
		- cluster1::\*>
	- Diag
		- set admin
		- set dev
		- cluster1::\*>

Node Shell is specific to a node 

![[Pasted image 20230321112533.png|600]]

# Physical Storage

![[Pasted image 20230321114144.png|600]]
If you scale the nodes you are scaling horizontally while scaling disks would be vertical scaling

- Disk Types 
	- Hard Disk Drives
		- moving parts 
		- slower
	- Solid State Drives
		- No moving parts
		- Faster

Controllers can have a mix of SSD / HDD or one type
a controller that just uses SSD is an all flash array FAS

```
disk show
aggr show
```

## Aggregates 

Aggregates is not just a grouping of disks but of raid groups ( 1 or more )
 - Aggregate
	 - Raid Groups
		 - Disks

## Raid Groups

have 1, 2 or 3 parity drives 
- RAID 4
	- one parity drive per raid group 
- RAID DP
	- two parity drives per raid group
- RAID TEC ( Triple Erasure Coding )
	- three parity drives per raid group

![[Pasted image 20230321115655.png|700]]


![[Pasted image 20230321115817.png|700]]



# Logical Storage

## Flexible Volumes
You cannot write data to an aggregate you need a flexible volume to do this
Full or thin provisioned
create/delete/mount/unmount/online/offline/grow/shrink 
Volumes are grouped together into a namespace which is a collection of volumes these do not have to be in the same aggregate and can be spread between nodes
Flexible volumes cannot span aggregtates



## Storage Virtual Machines
Before you create a volume you need a SVM
![[Pasted image 20230323075220.png|700]]


## Namespaces and Junction Paths
![[Pasted image 20230323075631.png|700]]

## Moving Volumes
Move from one aggregate to another within the same cluster
The src aggregate initiates the move and the destination is created 
Data is replicated from src to dest
A cutover takes places and activates the dest
Its transparent to clients


## Rehosting Volumes
Control of the vol moves from one SVM to another
This is disruptive to clients
Namespace of a volume changes
Note the data itself is not moved

![[Pasted image 20230323080344.png|700]]

# Networking Basics

## Networking ( Ports and LIFS )
A LIF is an entity that has may properties its not a piece of hw
	- address 
	- netmask
	- port
A LIF is configured on a port
A port is a physical card is a NIC in a slot named e0a e0b e0c etc
A LIF always belongs to a single SVM

There are also FC ports and the LIF is in the form of a World Wide Port Name WWPN

Have to add licenses one for each node as they are tied to serial numbers 

![[Pasted image 20230323081040.png|700]]

![[Pasted image 20230323081159.png|700]]


## Networking ( LIF Failover and Migration )

SAN LIFs cannot failover
NAS LIFS do failover
Cluster-mgmt LIF can failover within the node and to other nodes 
Node-mgmt LIF can failover only within the node

Failover is automatic
Migration is manual ( net int migrate )

You can revert a migrate ( net int revert )
auto revert is disabled by default

![[Pasted image 20230323081819.png|700]]


# Storage Protocols

What is NAS and SAN ?
![[Pasted image 20230323082046.png|700]]

![[Pasted image 20230323082217.png|700]]

![[Pasted image 20230323082411.png|700]]

Note SMB / CIFS synonymous

![[Pasted image 20230323082456.png|700]]

## NFS
WAFL : Write Anywhere File Layout this is the filesystem of the aggregate
Client needs a local mount point

![[Pasted image 20230323120506.png|700]]

### Client 
nfs-utils ( RedHat ) or nfs-common ( Debian )

### Server
NFS configured at the SVM layer
Requires a license 
![[Pasted image 20230323120730.png|700]]
There are a number of policy rules for NFS as below 
![[Pasted image 20230323120918.png|700]]


## CIFS
Common Internet FileSystem
SMB 1/2/3
For windows clients

![[Pasted image 20230323121528.png|700]]

Needs a license


## iSCSI

Client is the initiator and has a iqn number iscsi qualified name
Client logs into target and this needs an igroup for ONTAP

![[Pasted image 20230323122151.png|700]]


# Snapshots

A snapshot in ONTAP is a point i time copy of the active fs of a WAFL volume
you can have a 1000 snapshots
They are read only

## WAFL

WAFL always writes new blocks it never changes them
Filesystem is therefore always consistent

![[Pasted image 20230323123055.png|700]]

You can manually create snapshots , or scheduled or via third party tools 
- Manually
	- snap create
	- default snap time is 6 hours , 2 daily  and 2 weekly
	- snap restore 
	- snap restore-file

Restoring a full volume is not common this is really for restoring file(s)


