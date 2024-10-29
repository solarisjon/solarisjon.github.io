---
tags: 
netgroups: 
lead-engineer: 
manager(s): 
code_name: 
products:
---
## Types of air gaps

There are many variations on the air gap concept. At a high level, three main types are the most common:

- The total physical air gap—This is the salt mine type, which involves locking digital assets in a completely isolated physical environment, separated from any network-connected systems. A digital asset in a total physical air gap has no network connections. If anyone wants to get data from it or put data onto it, they must physically go to it, a process that usually involves going through physical security barriers.
    

- Segregated in the same environment—An air gap can be achieved by simply disconnecting a device from a network. One could have two servers on the same rack, for instance, but still air-gapped away from each other because one is not plugged into the network. 
    

- Logical air gap—A logical air gap refers to the segregation and protection of a network-connected digital asset by means of logical processes. For example, through encryption and hashing, coupled with role-based access controls, it is possible to achieve the same security outcomes that are available through a physical air gap. Even if someone can access the digital asset, the asset cannot be understood, stolen, or modified.




## Links


## Documentation


## Engineers (modify the query below)


```dataview
TABLE manager, office, grade
FROM "300 NetApp/People"
WHERE contains(products, "Charon") or contains(products, "IPSec")
```


## Notes
