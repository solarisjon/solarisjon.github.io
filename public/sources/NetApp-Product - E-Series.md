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

- On Call Manager for E-Series
	- https://netapp.sharepoint.com/sites/APBU/Engineering/ESSD/APCE/oncall/default.aspx?xsdata=MDV8MDJ8Q2hlay5UYW5AbmV0YXBwLmNvbXw5ZjFhYTk3N2I5Yjg0MTlkYWFiNDA4ZGM2ZWI5NzdkOHw0YjA5MTFhMDkyOWI0NzE1OTQ0YmMwMzc0NTE2NWIzYXwwfDB8NjM4NTA2OTkwMDUyNzE0NzYwfFVua25vd258VFdGcGJHWnNiM2Q4ZXlKV0lqb2lNQzR3TGpBd01EQWlMQ0pRSWpvaVYybHVNeklpTENKQlRpSTZJazFoYVd3aUxDSlhWQ0k2TW4wPXwwfHx8&sdata=WWNubW1BSUdzOUg1V3dtZSt5WVRRaUxhTnNtd3ZERktyOUpLdk5Vb2dGMD0%3d
- Support Engagement 
	- https://wikid.netapp.com/w/E-Series_Contacts

![](Assets/Eng%20On-Call%20Process%20Overview%20Oct%202024.pdf)


## 14th October 2024

### General Notes

eseries to mgr then to engineer
lynn fw manager

get system back not a rca 

terradata ( customer ) support usually handles these well 



### Questions

### Personal ToDos

### Action Items for Others 

---





## Engineers (modify the query below)


```dataview
TABLE office, grade, manager, organization, title
FROM ("300 NetApp/People")
WHERE contains(products, "E-Series") or (typeof(products) = "array" AND contains(products, [[NetApp-Product - E-Series]]))
sort office

```


## Notes
