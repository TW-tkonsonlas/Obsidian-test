<%
//Easy way to keep your templates from adding weird tags from your templater code
"---"%>
date: <%tp.date.now("YYYY-MM-DD",0)%>
modification date: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
links:<%*
//Grabbing the title of the document
heading = tp.file.title
//Split the Title by '_'
SplitTopics=heading.split('_');
//Grab the first section and make a link
company=`\n  - ${`\"\[\[${SplitTopics[0]}\]\]\"`}`;
-%><% company %>
aliases:
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]]

## Notes:
- <% tp.file.cursor(0) %>
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
