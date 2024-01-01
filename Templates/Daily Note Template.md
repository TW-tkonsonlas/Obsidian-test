<%"---"%>
date: <%tp.file.title%>
modification date: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
time: .5hr
links:<%*
//Grabbing the title of the document
heading = tp.file.title
//Split the Title by '_'
SplitTopics=heading.split('_');
//Grab the first section and make a link
subtopic1=`\n  - ${`\"\[\[${SplitTopics[1]}\]\]\"`}`;
//Split the Topic and Subtopic separated by the '.'
subsplit1=subtopic1.split('.');
//Form a link for the first 'Topic'
Topic1=`${subsplit1[0]}\]\]\"`;
//Create a link from the 'Topic and Subtopic'
subtopic2=`\n  - ${`\"\[\[${SplitTopics[2]}\]\]\"`}`;
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
tags:
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
[[Topic/Topic Index|Topic Index]]
## Notes:
- <%* tp.file.cursor(0) %>
## Tasks:
