<%"---"%>
date: <%tp.file.title%>
modification date: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
links:
  - "[[Daily]]"
lift: false
run: false
row: false
---
<< [[Daily/Map/<%moment(tp.date.now("YYYY-MM-DD",-1,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.now("YYYY-MM-DD",-1,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.now("YYYY-MM-DD",-1,tp.file.title,"YYYY-MM-DD")%>| Yesterday]] - <%tp.date.now("dddd",0,tp.file.title,"YYYY-MM-DD")%> - [[Daily/Map/<%moment(tp.date.now("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.now("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.now("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")%>|Tomorrow]] >>
`="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"` | [[Tasks and Backlog Items]] | [[Daily/Review/Weekly/<%moment(tp.date.weekday("YYYY-MM-DD",5,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%tp.date.weekday("YYYY-MM-DD",5,tp.file.title,"YYYY-MM-DD")%>| WeeklyReview]] | [[Topic/Topic Index|Topic Index]] | 
# Linked KeyNotes
```dataview
TABLE rows.L.text AS "KeyNote"
FROM outgoing([[]])
FLATTEN file.lists AS L
WHERE contains(L.tags, "#KeyNote")
GROUP BY file.link AS "File"
SORT File desc
```

# Daily Actions
- <% tp.file.cursor(1) %>
# Daily Side Notes
- 