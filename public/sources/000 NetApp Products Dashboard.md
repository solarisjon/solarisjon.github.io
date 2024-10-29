
```dataview
TABLE
from "300 NetApp/399 NetApp Products"
```


```dataview
TABLE products as Product, manager as Manager, timezone as TZ
from "300 NetApp/People"
where products != NULL
SORT TZ
```

000