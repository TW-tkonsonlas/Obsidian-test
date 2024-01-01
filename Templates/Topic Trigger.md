<%*
const folder = "Topic/Index";
const items = app.vault.getMarkdownFiles().filter(x=>x.path.startsWith(folder));
//This is where the question for the categories is posed
//let topic = await tp.system.suggester(topicpicker, topicpicker, true, "What is the Topic?")
const topic = (await tp.system.suggester((item) => item.basename,items)).basename;
//If 'Other' grab what the new Topic is
if (topic === "Other") {
  topic = await tp.system.prompt("Other Topic name:", "", true, false)
}
//If a user wants to add an Abbreviation to their links like a ticker for Companies
const abbpicker = ["Yes","No"]
//Default is "No"
let abbchoice = "No"
abbchoice = await tp.system.suggester(abbpicker, abbpicker, true, "Do you want to add an abbreviation?")
//If this is for a Sub Topic, what is it?
let abbreviation = ""
if (abbchoice === "Yes") {
  abbreviation = await tp.system.prompt("What is the abbreviation?", "", true, false)
}
//Check if this is for a new Sub Topic
const subtpicker = ["Yes","No"]
let subtchoice = "No"
subtchoice = await tp.system.suggester(subtpicker, subtpicker, true, "Is this for a sub-topic?")
//If this is for a Sub Topic, what is it?
let subtopic = ""
if (subtchoice === "Yes") {
  subtopic = await tp.system.prompt("What is the Sub Topic?", "", true, false)
}
//Creating the location variable
let location = ""
//Configuring the location based on the selection
//Constructing the 'name' of the file link
if (subtchoice === "Yes" && abbchoice === "Yes") {
  final_name = topic + "." + subtopic
  location = "Topic/SubTopic/"
} else if (subtchoice === "No" && abbchoice === "Yes") {
  final_name = topic + "." + abbreviation
  location = "Topic/Index/"
} else if (subtchoice === "Yes" && abbchoice === "No") {
  final_name = topic + "." + subtopic
  location = "Topic/SubTopic/"
} else { //subtchoice "No" abbchoice "No"
  final_name = topic
  location = "Topic/Index/"
}
//Building out the full path, file name, and then the shortened version of the link name
tR += "\[\[" + location + final_name + "\|" + final_name + "\]\]"
%> 