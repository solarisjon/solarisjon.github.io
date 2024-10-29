#NetApp #fabricpool #tiering #ONTAP #overview #netapp_products 

```toc

```

---

# Engineers

```dataview
TABLE manager, office, location
FROM "300 NetApp/People"
WHERE contains(products, "FabricPool")
```

---

## Overview

FabricPool is a storage tiering service for ONTAP its utilizes two tiering levels capacity and performance. 

Data that is frequently accessed remains in the performance tier and is backed by an aggregate of SSD drives in a FAS and AFF environment. When Cloud Volumes ONTAP ( [[CVO]] ) is used the drives in the aggregate can be a HDD but SSD is still recommended.
For data this not accessed frequently aka cold data it is moved to object storage either AWS, Azure, IBM Cloud or StorageGrid backed. In ONTAP 9.6 Alibaba Cloud and Google Cloud Platform were added.

A temperature scan monitors the activity of each block in the FabricPool aggregates and marks them as cold if they are not touched by the time interval specified for the tier.

A tiering scan collets the 4k blocks and packages them into 4Mb  objects to PUT in the object store

Note that FabricPool is not a backup mechanism and normal backups must be done.

There is a utility called Object Store Profiler that gives performance stats on the object storage 

Tiering policies are applied to volumes and there are four policies.

### Snapshot
This tier is available in ONTAP 9.2 and the default cooling interval is 2 days. This is also the *default* tiering policy.
This tiering policy tiers cold snapshot only blocks to the capacity tier after 2 days by default.
Blocks which are in both the active filesystem and a snapshot remain on the performance tier.
Note that you still need normal backups of the performance tier aggregate.

![[Pasted image 20230327175527.png]]

### Backup
This tier is available in ONTAP 9.4.
If you are in a DP volume, [[NetApp-Product - SnapMirror]] [[SnapVault]] relationship you can set a backup policy on the destination volume.

![[Pasted image 20230327180256.png]]
### Auto
This tier is available in ONTAP 9.4 the default cooling period is 31 days.
Metadata always remains the Performance tier.
		
![[Pasted image 20230327175626.png]]	

If you have an anti virus scan that touches all blocks you would want all blocks to be moved back to the performance tier, so this will only move blocks back in a random read

![[Pasted image 20230327175943.png]]

### None




Used for very sensitive data for example where it must not leave the building.

![[Pasted image 20230327180059.png]]



---
# Extra Notes

The `all` tiering policy, supported only on ONTAP 9.6 and later, moves all user data blocks in both the active file system and Snapshot copies to the cloud tier. It replaces the `backup` tiering policy.

---
# Training

https://www.youtube.com/watch?v=p_84mbHWB2s

---
# Documents

![[FabricPool Best Practice TR-4598.pdf]]


![[FP Tiering Impact on Snapmirror Performance.pdf]]