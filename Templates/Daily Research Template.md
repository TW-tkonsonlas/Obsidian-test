<%
//Easy way to keep your templates from adding weird tags from your templater code
"---"%>
date: <%tp.date.now("YYYY-MM-DD",0,tp.file.title,"YYYY-MM-DD")%>
modification date: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
links:<%*
//Grabbing the title of the document
heading = tp.file.title
//Building the name of the document for meetings
projectheading = heading.replace('Research','Project');
//Building the name of the document for research
meetingheading = heading.replace('Research','Meeting');
//Split the Title by '_'
SplitTopics=heading.split('_');
//Year from the title
year =`${SplitTopics[0]}`;
//Grab the first section and make a link
subtopic1=`\n  - ${`\"\[\[${SplitTopics[1]}\]\]\"`}`;
//Split the Topic and Subtopic separated by the '.'
subsplit1=subtopic1.split('.');
//Form a link for the first 'Topic'
Topic1=`${subsplit1[0]}\]\]\"`;
//Grab the secondary 'Topic and subtopic'
st2 =`${SplitTopics[2]}`;
//Creating a tag variable for adding to the Dataview searches below
st2tag = `\"#${st2.replace(/\s+/g,'_').replace(/\./g,'/')}\"`
//Modify the tag so that it can be added as frontmatter as well
st2tag_ = `\n  - ${st2tag}`
//Create a link from the 'Topic and Subtopic'
subtopic2=`\n  - ${`\"\[\[${st2}\]\]\"`}`;
//IF there was a '.' added in the name then run a split
if (subtopic2.includes(".")){
//Spit of the secondary Topic and Subtopic
	subsplit2=subtopic2.split('.');
	//Create a link for the Topic
	Topic2=`${subsplit2[0]}\]\]\"`;
	//Create a link for the subtopic like it was a Topic
	//Just in case it is decided to be made into a full topic later
	Topic3=`\n  - \"\[\[${subsplit2[1]}`;
	//Remove Topic3 if you don't want a hanging link
	tR += Topic2 + Topic3
}
//Below are the calls to create the frontmatter.
//As you can see with the st2tag, the variables can be used anywhere on the page
-%><% subtopic1 %><% Topic1 %><% subtopic2 %>
tags:<% st2tag_ %>
aliases:
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]] | [[Daily/Project/<% year %>/<% projectheading %>|<% projectheading %>]] | [[Daily/Meeting/<% year %>/<% meetingheading %>|<% meetingheading %>]]
## Notes:
- <% tp.file.cursor(0) %>
## Tasks:


## List Important Notes
```dataview
TABLE rows.L.text AS "Important Notes"
FROM [[#]]
AND "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Important")
AND contains(L.tags,<% st2tag %>)
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
AND contains(L.tags,<% st2tag %>)
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
AND contains(L.tags,<% st2tag %>)
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
AND contains(L.tags,<% st2tag %>)
GROUP BY file.link AS "File"
SORT File desc
```
## All Daily Links:
```dataview
TABLE
FROM [[#]]
SORT file.name desc
```