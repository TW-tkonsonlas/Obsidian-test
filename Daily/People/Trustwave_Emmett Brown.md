---
date: 2024-01-04
modification date: 2024-01-04 04:58:37
links:
  - "[[Trustwave]]"
aliases:
  - Dr Brown
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]]

## Notes:
- A bit eccentric, seems mostly reliable though 
## Tasks:


## Important Notes
```dataview
TABLE rows.L.text AS "Important Notes"
FROM [[#]]
AND "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Important")
AND (contains(file.outlinks,this.file.link)
	OR contains(file.inlinks,this.file.link))
GROUP BY file.link AS "File"
SORT File desc
```
## Key Notes
```dataview
TABLE rows.L.text AS "Key Note"
FROM [[#]]
AND "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#KeyNote")
AND (contains(file.outlinks,this.file.link)
	OR contains(file.inlinks,this.file.link))
GROUP BY file.link AS "File"
SORT File desc
```
## All Daily Links:
```dataview
TABLE
FROM [[#]]
AND "Daily"
SORT file.name desc
```
