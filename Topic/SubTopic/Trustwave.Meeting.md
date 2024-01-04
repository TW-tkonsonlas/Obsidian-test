---
date: 2024-01-01
modification date: 2024-01-01 11:53:53
aliases:
links:
  - "[[Trustwave]]"
  - "[[Meeting]]"
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]]
## List Important Notes
```dataview
TABLE rows.L.text AS "Important Notes"
FROM [[#]]
AND "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Important")
AND contains(L.text,"[[Trustwave.Meeting]]")
OR contains(L.text,"[[Trustwave.Meeting|")
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
AND contains(L.text,"[[Trustwave.Meeting]]")
OR contains(L.text,"[[Trustwave.Meeting|")
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
AND (contains(L.text,"[[Trustwave.Meeting]]")
	OR contains(L.text,"[[Trustwave.Meeting|"))
GROUP BY file.link AS "File"
SORT File desc
```
## Notes
```dataview
TABLE
FROM "Daily/Note"
Where contains(links,[[Trustwave.Meeting]])
SORT File desc
```
## All Daily Links:
```dataview
TABLE
FROM [[#]]
SORT file.name desc
```
## Projects
```dataview
TABLE
FROM "Daily/Project"
Where contains(links,[[Trustwave.Meeting]])
SORT File desc
```
## Meetings
```dataview
TABLE
FROM "Daily/Meeting"
Where contains(links,[[Trustwave.Meeting]])
SORT File desc
```
## Research
```dataview
TABLE
FROM "Daily/Research"
Where contains(links,[[Trustwave.Meeting]])
SORT File desc
```
## People
```dataview
TABLE
FROM "Daily/People"
Where contains(links,[[Trustwave]])
SORT File desc
```