<%
//Easy way to keep your templates from adding weird tags from your templater code
"---"%>
date: <%tp.date.now("YYYY-MM-DD",0)%>
modification date: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
aliases:<%*
//Grabbing the title of the document
heading=tp.file.title;
if (heading.includes(".")){
	//Split the Topic and Subtopic separated by the '.'
	split=heading.split('.');
	//Form a link for the first 'Topic'
	topic=`${split[0]}`;
	topic_a=`\n  - ${topic}`;
	topiclink=`\[\[${topic}\]\]`;
	abb=`${split[1]}`;
	abblink=`\[\[${split[2]}\]\]`;
	abb_a=`\n  - ${abb}`;
	//IF there was a '.' added in the name then run a split
	tR += abb_a + topic_a;
} else {
	topic=heading;
	topiclink=`\[\[${topic}\]\]`;
}
Project=`\[\[Topic\/SubTopic\/${topic}\.Project\|${topic}\.Project\]\]`;
Research=`\[\[Topic\/SubTopic\/${topic}\.Research\|${topic}\.Research\]\]`;
Meeting=`\[\[Topic\/SubTopic\/${topic}\.Meeting\|${topic}\.Meeting\]\]`;
Request=`\[\[Topic\/SubTopic\/${topic}\.Request\|${topic}\.Request\]\]`;
People=`\[\[Topic\/SubTopic\/${topic}\.People\|${topic}\.People\]\]`;
Proposal=`\[\[Topic\/SubTopic\/${topic}\.Proposal\|${topic}\.Proposal\]\]`;
%>
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]] | <% Project %> | <% Research %> | <% Meeting %>
 <% Request %> | <% People %> | <% Proposal %>
 <%* tp.file.cursor(0) %>
## List Important Notes
```dataview
TABLE rows.L.text AS "Important Notes"
FROM "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Important")
AND (contains(L.text,"[[<% topic %>]]")
	OR contains(L.text,"[[<% topic %>|"))
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
AND (contains(L.text,"[[<% topic %>]]")
	OR contains(L.text,"[[<% topic %>|"))
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
AND (contains(L.text,"[[<% topic %>]]")
	OR contains(L.text,"[[<% topic %>|"))
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
AND (contains(L.text,"[[<% topic %>]]")
	OR contains(L.text,"[[<% topic %>|"))
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
Where contains(links,<% topiclink %>)
SORT File desc
```
## Meetings
```dataview
TABLE
FROM "Daily/Meeting"
Where contains(links,<% topiclink %>)
SORT File desc
```
## Research
```dataview
TABLE
FROM "Daily/Research"
Where contains(links,<% topiclink %>)
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