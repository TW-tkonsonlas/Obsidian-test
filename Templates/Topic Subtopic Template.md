<%
//Easy way to keep your templates from adding weird tags from your templater code
"---"%>
date: <%tp.date.now("YYYY-MM-DD",0)%>
modification date: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
aliases:<%*
//Grabbing the title of the document
heading=tp.file.title;
//Split the Topic and Subtopic separated by the '.'
split=heading.split('.');
//Form a link for the first 'Topic'
topic=`\[\[${split[0]}\]\]`;
topic1=`\n  - ${`\"\[\[${split[0]}\]\]\"`}`;
subtopic=`${split[0]+"."+split[1]}`;
sublink=`\[\[${subtopic}\]\]`;
topic2=`\n  - ${`\"\[\[${split[1]}\]\]\"`}`;
%>
links:<% topic1 %><% topic2 %>
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
AND contains(L.text,"[[<% subtopic %>]]")
OR contains(L.text,"[[<% subtopic %>|")
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
AND contains(L.text,"[[<% subtopic %>]]")
OR contains(L.text,"[[<% subtopic %>|")
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
AND (contains(L.text,"[[<% subtopic %>]]")
	OR contains(L.text,"[[<% subtopic %>|"))
GROUP BY file.link AS "File"
SORT File desc
```
## Notes
```dataview
TABLE
FROM "Daily/Note"
Where contains(links,<% sublink %>)
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
Where contains(links,<% sublink %>)
SORT File desc
```
## Meetings
```dataview
TABLE
FROM "Daily/Meeting"
Where contains(links,<% sublink %>)
SORT File desc
```
## Research
```dataview
TABLE
FROM "Daily/Research"
Where contains(links,<% sublink %>)
SORT File desc
```
## People
```dataview
TABLE
FROM "Daily/People"
Where contains(links,<% topic %>)
SORT File desc
```