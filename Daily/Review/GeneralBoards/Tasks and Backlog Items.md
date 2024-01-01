 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]]
# All Tasks Not Completed
```dataview
Task
FROM "Daily"
WHERE !completed
AND text != ""
SORT due desc
```

# All BackLog
```dataview
TABLE rows.L.text AS "BackLog"
FROM "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#BackLog")
GROUP BY file.link AS "File"
SORT File desc
```


# Exercise Completed
```dataview
CALENDAR file.day
FROM "Daily/Map"
WHERE run = true
	OR lift = true
	OR row = true
```



