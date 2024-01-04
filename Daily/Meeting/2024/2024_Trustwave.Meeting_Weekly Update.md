---
date: 2024-01-01
modification date: 2024-01-04 05:17:09
links:
  - "[[Trustwave.Meeting]]"
  - "[[Trustwave]]"
  - "[[Weekly Update]]"
tags:
  - "#Weekly_Update"
aliases:
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]] | [[Daily/Project/2024/2024_Trustwave.Project_Weekly Update|2024_Trustwave.Project_Weekly Update]] | [[Daily/Research/2024/2024_Trustwave.Research_Weekly Update|2024_Trustwave.Research_Weekly Update]]
## Notes:
- 
## Tasks:


## List Important Notes
```dataview
TABLE rows.L.text AS "Important Notes"
FROM [[#]]
AND "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Important")
AND contains(L.tags,"#Weekly_Update")
GROUP BY file.link AS "File"
SORT File desc
```
## List Key Notes
```dataview
TABLE rows.L.text AS "Key Note"
FROM [[#]]
AND "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#KeyNote")
AND contains(L.tags,"#Weekly_Update")
GROUP BY file.link AS "File"
SORT File desc
```
## List Links
```dataview
TABLE rows.L.text AS "Links"
FROM [[#]]
AND "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Link")
AND contains(L.tags,"#Weekly_Update")
GROUP BY file.link AS "File"
SORT File desc
```
## List Notes
```dataview
TABLE rows.L.text AS "Notes"
FROM [[#]]
AND "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Note")
AND contains(L.tags,"#Weekly_Update")
GROUP BY file.link AS "File"
SORT File desc
```
## All Daily Links:
```dataview
TABLE
FROM [[#]]
SORT file.name desc
```