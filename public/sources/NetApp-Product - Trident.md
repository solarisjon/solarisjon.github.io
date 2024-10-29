

# Notes from the CPE-6332 Juniper Case

Prior to version 23.04 Trident used per-backend igroups.  In rare instances iSCSI self-healing didn’t complete leaving stale devices.  
Stale devices could lead to data/filesystem corruption and read-only volumes.  
The below Service Bulletin summarizes and describes this issue as well as how to confirm devices are in this state.
[https://kb.netapp.com/Support_Bulletins/Customer_Bulletins/SU535](https://kb.netapp.com/Support_Bulletins/Customer_Bulletins/SU535 "https://kb.netapp.com/Support_Bulletins/Customer_Bulletins/SU535")
Beginning with version 23.04 Trident began using per-node igroups.  The data provided confirms there are no more per-backend igroups in use on your ONTAP clusters.  
iSCSI self-healing works well with per-node igroups so device cleanup on unmount should no longer be an issue, but this does not address earlier stale devices.  
Version 23.07.1 enhanced ZAPI requests to ONTAP ensuring LUN serial numbers are queried when getting LUN attributes to identify and fix stale iSCSI devices during Node Staging operations.  
Version 23.07.1 should resolve data/filesystem corruption issues as well as read-only issues caused by stale devices.  
Juniper is strongly encouraged to upgrade their Trident deployment to version 23.07.1 at the soonest opportunity.
iSCSI self-healing has been enhanced in version 24.06 to initiate SCSI scans by exact LUN ID if deprecated igroups are in use to clean up stale devices.  
Prior to version 24.06 any mount issues caused by stale device will need to be identified and cleared manually.

Self-healing cannot be disable before Trident v24.02, however Trident v23.07.1 will check for and not mount stale/zombie dm devices.  It should not be necessary to test Trident for the ONTAP upgrade RO scenario after upgrading Trident to v23.07.1.

Self-healing can be disabled by setting the self-healing interval to 0s.  The method depends on installation method and version.  
This is a tridentctl installation, which Trident version will you be testing with 23.04 or 23.07.1?
The Service Bulletin linked below shows the steps to identify stale DM devices.
Please allow me time to test these steps in my lab first.
Find the volume name
   oc get pvc -n name-space
List multipath devices.
   multipath -ll
In ONTAP, confirm volumes are mapped to the correct igroup
   lun show -fields path, serial-hex, mapped

```dataview
TABLE manager, office, grade
FROM "300 NetApp/People"
WHERE contains(products, "Trident")
```

