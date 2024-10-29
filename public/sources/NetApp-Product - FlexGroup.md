
#netapp #product #netapp_products 


# Engineers



```dataview
TABLE manager, office, title, organization
FROM "300 NetApp/People"
WHERE contains(products, "FlexGroup") or (typeof(products) = "array" AND contains(products, [[NetApp-Product - FlexGroup]]))
sort office
```


# Notes

Allow you to have volumes of a larger size than normally available 
Better Performance 

FlexVols 
	- aggregates and their disks are owned by a single node
	- flexvols contained in one aggregate 
	- flexvols cannot span aggregates or nodes so size is limited
	- max size is controller dependent
	- FAS9000 - max aggregate size is 400TB but with FlexVol size is 100TB

Infinite Volumes 
	- Available in ONTAP 8.1.1 spans aggregates and nodes
	- SMB1.0 NFSv3 pNFS and NFSv4.1 are supported 
	- Single scalable volume that store up to 2 billion files and up to 20Pb of data
	- dedicated SVM

No SAN support only NAS for Infinite Volumes 

