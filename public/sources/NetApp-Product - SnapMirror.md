
#NetApp #snapmirror #snapshots #learning #netapp_products 

---

```toc
```

---
# Engineers

```dataview
TABLE manager, office, grade
FROM "300 NetApp/People"
WHERE contains(products, "SnapMirror") or (typeof(products) = "array" AND contains(products, [[NetApp-Product - SnapMirror]]))
```

---
# Training

```embed
title: ''
image: 'https://www.google.com/favicon.ico'
description: 'About this page'
url: 'https://youtu.be/kjdiPF4mD7U'
```

---
# Documents

## FlexGroup SnapMirror initialization is failing with ONTAP 9.11.1 or later to use this feature
1. [](https://kb.netapp.com/@api/deki/pages/69967/pdf/FlexGroup%2bSnapMirror%2binitialization%2bis%2bfailing%2bwith%2bONTAP%2b9.11.1%2bor%2blater%2bto%2buse%2bthis%2bfeature.pdf?stylesheet=default "Export page as a PDF")
https://kb.netapp.com/onprem/ontap/dp/SnapMirror/FlexGroup_SnapMirror_initialization_is_failing_with_ONTAP_9111_or_later_to_use_this_feature

![](Assets/FSx%20SM-C%20Performance%20July%2003%202023%20--%20shared.pdf)

---
# Product Variations

- SnapMirror (SM) : ONTAP -> ONTAP
- ( LSRE ) : FSx -> FSx
- SnapMirror Cloud (SM-C) : FSx -> S3 datastore

---



# Asynchronous Volume SnapMirror

![[Pasted image 20230315135114.png|700]]

- Source Volume ( type=rw vol)|500
- Destination Volume ( type=dp vol Data Protection )
- Source and destination will be in two different SVM's and two different clusters
- When you create a relationship its of a particular type 
	- XDP ( default ) vault relationship for backups
	- DP for disaster recovery 
	- LS for load share
	- TDP for transition data protection (used for 7mode to ONTAP)
- Schedule is vital component of the relationship
	- based on the schedule a snapshot will be created on the source and all the blocks replicated on the dest
- Snapmirror Policy is connected to the relationship
	- multiple rules
		- Keep param : how many snapshots to keep on the destination
		- SnapMirror label field during an update the source volume will be scanned with this label


# Automated Data Tiering in the Cloud

```embed
title: 'watch?v=gVlV3kMk7MI'
image: 'https://img.youtube.com/vi/gVlV3kMk7MI/maxresdefault.jpg'
description: ''
url: 'https://www.youtube.com/watch?v=gVlV3kMk7MI'
```


# ONTAP Cloud

![[Pasted image 20230403181600.png|600]]

![[Pasted image 20230403181641.png]]

![[Pasted image 20230403181713.png|900]]

![[Pasted image 20230403182007.png|1000]]
VPC provides a secure endpoint 
Tiering between performance tier or your data aggregate on your ONTAP cloud system and your S3 bucket is to create a VPC endpoint with the S3 svc 
When you replicate via SM you can replicate to your ONTAP system drop some metadata to the performance tier and the data to the S3

![[Pasted image 20230403182614.png|1000]]

## ONTAP Cloud Tiering

![[Pasted image 20230403182833.png|1000]]

---
# Default Schedules For SnapShots ( #snapshots)
|  | 6 hourly – Taken at the top of each hour – for every volume, every hour we capture a snapshot, with 6 snapshot being kept. |
|---|----------------------------------------------------------------------------------------------------------------------------|
|  | 2 daily – Taken at midnight, 2 dailies kept                                                                                |
|  | 2 weekly – Sunday at midnight                                                                                              |
