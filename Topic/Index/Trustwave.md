---
date: 2023-12-28
modification date: 2023-12-28 08:47:53
aliases:
  - TW
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]] | [[Topic/SubTopic/Trustwave.Project|Trustwave.Project]] | [[Topic/SubTopic/Trustwave.Research|Trustwave.Research]] | [[Topic/SubTopic/Trustwave.Meeting|Trustwave.Meeting]]
 [[Topic/SubTopic/Trustwave.Request|Trustwave.Request]] | [[Topic/SubTopic/Trustwave.People|Trustwave.People]] | [[Topic/SubTopic/Trustwave.Proposal|Trustwave.Proposal]]
 
## List Important Notes
```dataview
TABLE rows.L.text AS "Important Notes"
FROM "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Important")
AND (contains(L.text,"[[Trustwave]]")
	OR contains(L.text,"[[Trustwave|"))
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
AND (contains(L.text,"[[Trustwave]]")
	OR contains(L.text,"[[Trustwave|"))
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
AND (contains(L.text,"[[Trustwave]]")
	OR contains(L.text,"[[Trustwave|"))
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
AND (contains(L.text,"[[Trustwave]]")
	OR contains(L.text,"[[Trustwave|"))
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
## Projects
```dataview
TABLE
FROM "Daily/Project"
Where contains(links,[[Trustwave]])
SORT File desc
```
## Meetings
```dataview
TABLE
FROM "Daily/Meeting"
Where contains(links,[[Trustwave]])
SORT File desc
```
## Research
```dataview
TABLE
FROM "Daily/Research"
Where contains(links,[[Trustwave]])
SORT File desc
```

## Subtopics
```dataview
TABLE
FROM "Topic/SubTopic"
Where contains(file.outlinks,this.file.link)
OR contains(file.inlinks,this.file.link)
SORT File desc
```