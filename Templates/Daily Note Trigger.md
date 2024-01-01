<%*
//This is where the question for the subcategories is posed
//The order here is the order that they will be presented
const folder = "Topic/Index";
const items = app.vault.getMarkdownFiles().filter(x=>x.path.startsWith(folder));
const topic = (await tp.system.suggester((item) => item.basename,items)).basename;
//Here is where the subtopic is grabbed
//The order here is the order that they will be presented
const subtpicker = ["Meeting","Request","Project","Research","People","Proposal"]
let subtopic = await tp.system.suggester(subtpicker, subtpicker, true, "What kind of action is it?")
//Here is where the subcategories are managed
//The order here is the order that they will be presented
const noteCheck = ["Note","New"]
let note = "Note"
if (subtopic === "Project") {
  note = await tp.system.suggester(noteCheck, noteCheck, true, "Is this a new Project group or a Note?")
} else if (subtopic === "Meeting") {
  note = await tp.system.suggester(noteCheck, noteCheck, true, "Is this a new Meeting group or a Note?")
} else if (subtopic === "Research") {
  note = await tp.system.suggester(noteCheck, noteCheck, true, "Is this a new Research group or a Note?")
}
let subject = ""
subject = await tp.system.prompt("Subject:", "", true, false)
//Grab the date for location and title
let held = tp.date.now("YYYY-MM-DD", 0, tp.file.title, "YYYY-MM-DD")
let year = moment(tp.date.now("YYYY-MM-DD",0,tp.file.title,"YYYY-MM-DD")).format('YYYY')
let month = moment(tp.date.now("YYYY-MM-DD",0,tp.file.title,"YYYY-MM-DD")).format('MM')
//Configuring the location based on the selection
//Constructing the 'name' of the file link
let location = ""
if (note === "New") {
//Create the subject in a new Group and put in the appropriate folder
  if (subtopic === "Project") {
	  final_name = year + "_" + topic + "." + subtopic + "_" + subject
	  location = "Daily/Project/" + year + "/"
	  } else if (subtopic === "Meeting") {
	  final_name = year + "_" + topic + "." + subtopic + "_" + subject
	  location = "Daily/Meeting/" + year + "/"
	  } else {//subtopic === Research
	  final_name = year + "_" + topic + "." + subtopic + "_" + subject
	  location = "Daily/Research/" + year + "/"
  }
} else if (subtopic === "People"){
  final_name = topic + "_" + subject
  location = "Daily/People/"
} else {
  final_name = held + "_" + topic + "." + subtopic + "_" + subject
  location = "Daily/Note/" + year + "/" + month + "/"
}
//Building out the full path, file name, and then the shortened version of the link name
tR += "\[\[" + location + final_name + "\|" + final_name + "\]\]"
%> 