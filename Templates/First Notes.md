## Plugins
- Dataview(Install)
- Templater(Install)
### Optional
- Tasks (Enjoy the task creation GUI)
## Settings Obsidian
- Settings->Files and links->
	- Automatically update internal links
		- Enabled
	- Default location for new notes
		- 'In the folder specified below'
		- "Topic/Index"
	- Default location for new attachments
		- 'In the folder specified below'
		- "Topic/xAttachments"(Or wherever you want to stash these)
- Settings->Core plugins->
	- Daily notes
		- Disable(This will be managed by Templater)
	- Templates
		- Disable(This will be managed by Templater)
- Settings->Community plugins
	- If you didn't enable the installed plugins when you grabbed them
		- Enable all installed community plugins
- **Preference**
- Settings->Appearance
	- Base color scheme
		- Dark
	- Font Size
		- 13
- **!!! IMPORTANT !!!**
- Settings->Fire recovery
	- Get familiar with this core plugin, super handy, rarely see mention of this
	- Just know that it is there, and if you want modify the settings
- **Plugin Settings**
- Templater
	- Automatic jump to cursor
		- enabled
	- Trigger Templater on new file creation
		- enabled
	- Template HotKeys
		- Templates/Daily Note Trigger(ctrl+2)
		- Templates/Topic Trigger(ctrl+3)
	- Enable Folder Templates(This is the primary piece leveraged for this vault)
		- See 'Templater Templates'
### Templater Templates:
- Daily/Map: Templates/Daily Map Template
- Daily/Note: Templates/Daily Note Template
- Daily/Review/Weekly: Templates/Summary Weekly
- Daily/Review/Monthly: Templates/Summary Monthly
- Daily/Project: Templates/Daily Project Template
- Daily/Meeting: Templates/Daily Meeting Template
- Daily/Research: Templates/Daily Research Template
- Daily/People: Templates/Daily People Template
- Topic/Index: Templates/Topic Index
- Topic/Subtopic: Templates/Subtopic
## Current Hotkeys
### Critical
ctrl + 1: Pin current tab
	Not really critical, but handy to have so you don't navigate away from core notes
ctrl + 2: Daily Note Trigger
	This is the default trigger you will use daily to create new notes. I try to avoid actually adding any notes within the 'Daily Map'.
ctrl + 3: Topic Trigger
	This is something still being worked. But it will let you manually create either a Topic or a trigger.
ctrl + t: Create a new Task
ctrl + .: Add bullet to selected lines
	Dataview works around lists, lines beginning with a bullet, to be able to pull the tagged data. There are some other options also available, but this seems to be the cleanest I have found at the moment.
### Nice to have
ctrl + -: Fold Heading
ctrl + shift + -: Fold All Headings
ctrl + =: UnFold Heading
ctrl + shift + =: UnFold All Headings
ctrl + r: search and replace text
### General Tags leveraged
#Action 
#BackLog
#Important 
#KeyNote 
#Note 
#Link 

### How I use these notes
#### Basics
The 'Daily' section is where all actual data and notes reside.
The 'Templates' are where just the templates for all notes live
And the 'Topic' folder is just supposed to be essentially boards/views created to view your data/notes.

#### First Step
From this page, AFTER you have the folder structure in place and you also have linked all of the templates to the appropriate folders, you can click on the links below to trigger you first files to be created.
`="[["+ "Daily/Map" + "/" + dateformat(date(today), "yyyy") + "/" + dateformat(date(today), "MM") + "/" + dateformat(date(today), "yyyy-MM-dd") + "| Active Daily Map"+"]]"` : [[Topic/Topic Index|Topic Index]] : [[Tasks and Backlog Items]]
Check out each of these files and the Dataview code. At the moment it is all very simple code so that it easy to kind of see what you will have to work with. Since everyone will leverage the notes differently, I'm sure everything will be leveraged differently.
#### Default view
Now that you should have the basic 3 files in place, I recommend opening up your 'Active Daily Map' in another tab. Pin that note so that it can't be closed or navigated away from. Next from that note, right click the 'Tasks and Backlog Items' link and click 'Open to the right'. Should be the third option down from the top. Pin that file on the right.
With the daily map on the left and the tasks and backlog items on the right, this is the default driving view I have been using.
#### Creating a topic
To get started, add at least one 'Topic'. Since I intend to use these notes for work, my default topic is my company. Type two square brackets, the name of your company, followed by two closing square brackets and a space. Now you should see the link you've created, though it doesn't lead anywhere yet.

If you've set up default file creation correctly, clicking on the link should create a file under 'Topic/Index', formatted with the 'Topic Template'.

Next, click on the links at the top for at least 'Meeting', 'Project', and 'Research'. Explore the file and observe how Dataview queries, aliases, and YAML are set up. While it's still basic, use this first file to compare with the Topic Template to understand how JavaScript could be leveraged. Notice how you can create a stack of variables at the top and then leverage them throughout the file.
#### Creating a note
I organize my notes using the 'Daily Map' under the 'Daily Actions' header. On the first line with a bullet, I press Ctrl + 2 to trigger the 'Daily Note Trigger'. You should see your Topic created from the previous step, along with any other topics you have. Choose the topic of interest, and you'll be presented with a list of core actions to perform. Feel free to modify the 'Daily Note Trigger' to add or remove actions as needed.

For this example add a 'Meeting', select 'Note', and type out a sample meeting name.

Now, you have your first note link. Before clicking on the link, add the #Action tag after the link. Then, open the note.

#### Building a note
In the first note, you'll find links to 'Topic.Meeting,' 'Topic,' and a link for the 'Subject' you created. I've mostly left the 'subject' as a hanging link to nothing, but in cases where I want the subject to be a topic, I can quickly click on the link to create a topic. If the subject is a recurring item or something else, it's automatically linked to other notes covering the same 'subject.' Keep in mind that this is limited by what you put into the header and can't automatically include everything you might want or need in this list of links. I manually add links to related notes as needed.

Regarding tags, I've generally avoided them except as a way to group Meeting/Project/Research notes around a central idea that I don't want to make a topic out of. For example, if I start a project for my company like 'Updating SOPs,' I don't want a topic for that, but I want another way to group actions/notes around those activities without creating a topic. It's not a perfect model, and ideally, I want to move away from these tags, but for now, they address a problem I haven't found a good solution for yet.

To add a note, just type something under the header 'Notes:' and add the #KeyNote tag to the line. Navigate back to your Daily Map, and you can see that KeyNote.

I envision leveraging this by jumping into a meeting, using a method like the Cornell Note method and employing active listening. Only add notes for things that truly matter. Address the points during the meeting or recap after the meeting, adding appropriate tags like #Note for a low-level note, #KeyNote for a mid-tier action, and #Important for something with a lasting effect that needs to be remembered. For questions, I use #KeyNote for something to take action on within the next 24 hours, or create a task. If it's something I need to address but won't have time in the next 24 hours, I leverage the #BackLog tag. This approach is extremely subjective and dependent on everyone's own workflow.

#### Conclusion
Now you have the super bare bones of these notes.

I didn't delve into 'SubTopic,' 'People,' or 'xArchive.' I also haven't outlined how I search for code snippets, manage links, perform basic web scraping and cataloging, or use LLMs like ChatGPT. This is because I'm still figuring out those aspects and modifying how I utilize everything mentioned above.

The method presented here is just one approach to leveraging links—a starting point without having to build everything from scratch, mainly relying on only two plugins: Dataview and Templater. I intend to continually refine this basic setup throughout 2024 to fully understand what I can achieve with just JavaScript, links, planned templates, and some Dataview queries to pull notes of interest.

Before adding more advanced plugins, I believe it's time well spent to comprehend the fundamental functions and establish a clear concept of how to track notes.
