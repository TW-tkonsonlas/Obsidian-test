---
date: <%tp.file.title%>
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("Y HH:mm:ss") %>
tags:
  - "#DailyNote"
Run: false
Row: false
Lift: false
---
# Current Hotkeys
ctrl + 1: Pin current tab
ctrl + 2: Action Trigger
ctrl + 3: Inline Complete+date
ctrl + -: Fold Heading
ctrl + shift + -: Fold All Headings
ctrl + =: UnFold Heading
ctrl + shift + =: UnFold All Headings
ctrl + .: Add bullet to selected lines
ctrl + t: Create a new Task
ctrl + r: search and replace text
ctrl + h: highlight selected text


<%*
type = tp.file.title;
thirdDashIndex=type.indexOf('-',type.indexOf('-',type.indexOf('-')+1)+1);
fourthDashIndex=type.indexOf('-',thirdDashIndex+1);
extractedString=fourthDashIndex !== -1?type.substring(thirdDashIndex+1,fourthDashIndex):type.substring(thirdDashIndex+1);
name=extractedString.replace(/\s+/g,'/')?`\"#${extractedString.replace(/\s+/g,'/')}\"`:"";
tR+=name
-%>
# Dataview table from list using Link
```dataview
TABLE rows.L.text AS "BackBurner"
FROM "Daily"
FLATTEN file.lists AS L
WHERE contains(L.text, "[[BackBurner]]")
AND contains(L.text, "[[Legacy_Analytics]]")
AND !contains(L.tags,"#Status/Complete")
GROUP BY file.link AS "File"
SORT File desc
```

# Task table using 'Task'
```tasks
not done
hide backlink
sort by due asc
```

# Font Color Change
<%*
const colors = ['green','red','yellow','blue'];
let color = await tp.system.suggester(colors,colors,false,'Color');
if (color !== null)
{
tR = `<font color=${color}>${tp.file.selection()}</font>`
}
-%> 

# Inline Categories Trigger
<%*
const categories = ["BackBurner","Python","PythonLink","PowerShell","PowerShellLink","Research","ResearchLink","Sentinel","SentinelLink","KQL","KQLLink","Obsidian","ObsidianLink",]
let type = await tp.system.suggester(categories, categories, true, "Pick an inline catagory to print:",10)

final_name = type + "\:\:"
tR += final_name
%> 

# Inline Completed Date
<%*
type = "Completed"
date = tp.date.now("YYYY-MM-DD")
final_name = type + "\:\: " + date
tR += final_name
%>
# Dataview Filter based on Property
```dataview
TABLE
FROM "Daily"
WHERE contains(date, "2023-12-18")
```

[[<% tp.date.now("YYYY-MM-DD") %>]] 

<% tp.file.folder%>

Autoset a tag based on the title, v1.0
<%* let type = tp.file.title; name = (type.includes("Meeting")) ? "\"\#Meeting\"" :(type.includes("Project")) ? "\"\#Project\"" : (type.includes("Request")) ? "\"\#Request\"" :(type.includes("Research")) ? "\"\#Research\"" : ""; tR += name %>

<%* let type = tp.file.title;
// Find the position of the third '-' occurrence
thirdDashIndex = type.indexOf('-', type.indexOf('-', type.indexOf('-') + 1) + 1);

// Find the position of the fourth '-' occurrence
fourthDashIndex = type.indexOf('-', thirdDashIndex + 1);

// Extract the substring from the third '-' to the fourth '-'
extractedString = fourthDashIndex !== -1 ? type.substring(thirdDashIndex + 1, fourthDashIndex) : type.substring(thirdDashIndex + 1);

// Replace spaces with '/' and create the final name
name = extractedString.replace(/\s+/g, '/') ? `\"#${extractedString.replace(/\s+/g, '/')}\"` : "";
tR += name %>


# tp.config

# tp.file
Grabs the title of the file
<% tp.file.title %>
To automatically set the cursor in a specific place when the template is opened
<% tp.file.cursor() %>
Script to grab the title when a new file is created
<%*
	let title = tp.file.title 
	if (title.startsWith("Untitled")) {
		title = await tp.system.prompt("Title");
		await tp.file.rename(`${title}`);
	}
%>
# <%* tR += `${title}` %>

Sample Code---
`<%* let day =` [tp.date.now](https://tp.date.now)`("dd")`

`if ((day != "Sa") && (day != "Su")) { %>`

`# Agenda`

`<%* } else { %>`

`<%* } %>`
---
# tp.date 
# tp.frontmatter

# tp.hooks

# tp.obsidian

# tp.system

# tp.web


Search "replace"
	replace templates in the active file
	<% tp.date.now("YYYY-MM-DD")%> - <% tp.file.title %>

<% tp.user.script("Hey there") %>

setup a template to create a new file within a specific folder, and then leverage a link to possibly automatically create a new file within a folder with the desired name and meta data
<< [[Daily/Notes/<% await moment(tp.date.now("YYYY-MM-DD",-1,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<% await moment(tp.date.now("YYYY-MM-DD",-1,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<% await moment(tp.date.now("YYYY-MM-DD",-1,tp.file.title,"YYYY-MM-DD").format('WW') - - 1%>| LastWeek]] 

- <% await tp.file.title %> - [[Daily/Notes/<% await moment(tp.date.now("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<% await moment(tp.date.now("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<% await tp.date.now("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")%>|NextWeek]] >>


---
<%*

let type, name, topic, held
held = tp.date.now("YYYY-MM-DD")
topic = "o "
type = await tp.system.suggester(["with a specific person", "meeting with a custom name", "no specific people nor names"], ["with a specific person", "meeting with a custom name", "no specific people nor names"], false, "What kind of meeting it was?")

if (type == "with a specific person") name = await tp.system.prompt("What was their first and second name?", "with ", true, false)
else if (type == "meeting with a custom name") name = await tp.system.prompt("What was the meeting called then?", "", true, false)
else if (type == null || type == "no specific people nor names") name = "" 

topic = await tp.system.prompt("What was the meeting about?", "about ", true, false)
if (topic == "about ") topic = ""

let final_name = name
if (name.length > 0) final_name += " "

let triggered_date = tp.date.now("YYYY-MM-DD", 0, tp.file.title, "YYYY-MM-DD")
if (held != triggered_date) {
	if (await tp.system.prompt("You triggered this meeting in a note from " + triggered_date + ". Do you want to use this date instead of today's? y / ESC", false, false, false) == "y") held = triggered_date
}

final_name += topic + " - " + held

tR += "!\[\[" + final_name + "\]\]"
tp.file.create_new(tp.file.find_tfile("new meeting"), final_name, true, app.vault.getAbstractFileByPath("meetings"))

%>

---

<%*if (tp.file.title contains "Meeting") name = "#Meeting" else if (type == "meeting with a custom name") name = await tp.system.prompt("What was the meeting called then?", "", true, false) else if (type == null || type == "no specific people nor names") name = "" tR += name%>


```dataview
TABLE ResearchLink
FROM "Daily/Notes"
WHERE contains(ResearchLink, "#Person/Podcast/SteveGibson")
AND ResearchLink != null
```

```tasks
path includes Notes
tags include Gibson
```

```dataview
TABLE
FROM "Daily"
FLATTEN file.lists AS L
WHERE contains(L.text, "#Person/Podcast/SteveGibson")
```
