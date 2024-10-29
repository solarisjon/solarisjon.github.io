---
tags: 
netgroups: 
lead-engineer: 
manager(s): 
code_name: 
products:
---

## Links


## Documentation


Multi-Disk Panic.   In a traditional on prem system, with RAID-DP, 3 or more disks in a RAID group are inaccessible/failed for some reason.  One typical scenario is where two disks are in reconstruction and a third disk fails.  In this particular scenario it looks like there is something more fundamentally wrong because many disks were inaccessible.   Could be hardware connectivity or something related to that headswap and system ids.  It appears that disks may be showing as being owned by the prior MotherBoard, for example.  (When you do a headswap, part of the procedure needs to re-assign the proper disks to the new MotherBoard sysid.)

If David was around, I would have asked him to follow up.  In his absence, decided to request an escalation.  An MDP corefile is usually not enough to tell you what is going on/what happened.  We know disks failed or where inaccessible, but the question is why and how to recover (if the system did not recover upon reboot).



## Engineers (modify the query below)



## Notes
