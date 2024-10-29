
#NetApp #netapp_products 


# Links

- https://wikid.netapp.com/w/WAFL/WAFLReadWrite
- https://wikid.netapp.com/w/Directory-Indexing-TOI
- 
# CPE Engineers


```dataview
TABLE office, grade, manager, organization
FROM ("300 NetApp/People")
WHERE contains(products, "WAFL") or (typeof(products) = "array" AND contains(products, [[NetApp-Product - WAFL]]))
sort office

```


