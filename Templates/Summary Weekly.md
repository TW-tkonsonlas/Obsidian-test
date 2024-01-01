<%"---"%>
date: <%tp.file.title%>
modification date: <% tp.file.last_modified_date("Y HH:mm:ss") %>
links:
  - "[[WeeklySummary]]"
---
 `="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"`
<< [[Daily/Review/Weekly/<%moment(tp.date.weekday("YYYY-MM-DD",-2,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%tp.date.weekday("YYYY-MM-DD",-2,tp.file.title,"YYYY-MM-DD")%>| LastWeek]] - <%tp.date.weekday("YYYY",5,tp.file.title,"YYYY-MM-DD") %>-W<% tp.date.weekday("WW",5,tp.file.title,"YYYY-MM-DD") - -1%> - [[Daily/Review/Weekly/<%moment(tp.date.weekday("YYYY-MM-DD",12,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%tp.date.weekday("YYYY-MM-DD",12,tp.file.title,"YYYY-MM-DD")%>|NextWeek]] >>
Days: [[Daily/Map/<%moment(tp.date.weekday("YYYY-MM-DD",0,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.weekday("YYYY-MM-DD",0,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.weekday("YYYY-MM-DD",0,tp.file.title,"YYYY-MM-DD")%>| Sun]]|[[Daily/Map/<%moment(tp.date.weekday("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.weekday("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.weekday("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")%>| Mon]]|[[Daily/Map/<%moment(tp.date.weekday("YYYY-MM-DD",2,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.weekday("YYYY-MM-DD",2,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.weekday("YYYY-MM-DD",2,tp.file.title,"YYYY-MM-DD")%>| Tue]]|[[Daily/Map/<%moment(tp.date.weekday("YYYY-MM-DD",3,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.weekday("YYYY-MM-DD",3,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.weekday("YYYY-MM-DD",3,tp.file.title,"YYYY-MM-DD")%>| Wed]]|[[Daily/Map/<%moment(tp.date.weekday("YYYY-MM-DD",4,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.weekday("YYYY-MM-DD",4,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.weekday("YYYY-MM-DD",4,tp.file.title,"YYYY-MM-DD")%>| Thu]]|[[Daily/Map/<%moment(tp.date.weekday("YYYY-MM-DD",5,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.weekday("YYYY-MM-DD",5,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.weekday("YYYY-MM-DD",5,tp.file.title,"YYYY-MM-DD")%>| Fri]]|[[Daily/Map/<%moment(tp.date.weekday("YYYY-MM-DD",6,tp.file.title,"YYYY-MM-DD")).format('YYYY')%>/<%moment(tp.date.weekday("YYYY-MM-DD",6,tp.file.title,"YYYY-MM-DD")).format('MM')%>/<%tp.date.weekday("YYYY-MM-DD",6,tp.file.title,"YYYY-MM-DD")%>| Sat]]
# Actions from the Week
```dataview
TABLE rows.L.text AS "Actions"
FROM "Daily/Map"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#Action")
	AND file.day >= date(<%tp.date.now("YYYY-MM-DD",-6,tp.file.title,"YYYY-MM-DD")%>)
	AND file.day <= date(<%tp.date.now("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")%>)
GROUP BY file.link AS "File"
```
# BackLog from the Week
```dataview
TABLE rows.L.text AS "BackLog"
FROM "Daily"
FLATTEN file.lists AS L
WHERE contains(L.tags, "#BackLog")
	AND file.day >= date(<%tp.date.now("YYYY-MM-DD",-6,tp.file.title,"YYYY-MM-DD")%>)
	AND file.day <= date(<%tp.date.now("YYYY-MM-DD",1,tp.file.title,"YYYY-MM-DD")%>)
GROUP BY file.link AS "File"
```

<% tp.file.cursor(0) %>